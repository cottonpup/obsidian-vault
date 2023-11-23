
- [[#📒 427. Redux & Side Effects (and Asynchronous Code)]]
- [[#📒 428. Refresher / Practice Part 1/2]]
- [[#📒 429. Refresher / Practice Part 2/2]]
- [[#📒 430. Redux & Async Code]]
- [[#📒 431. Frontend Code vs Backend Code]]
- [[#📒 432. Where To Put Our Logic]]
- [[#📒 433. Using useEffect with Redux]]
- [[#📒 434. A Problem with useEffect()]]
- [[#📒 435. Handling Http States & Feedback with Redux]]
- [[#📒 436. Using an Action Creator Thunk]]
- [[#📒 437. Finalizing the Fetching Logic]]
- [[#📒 438. Getting Started with Fetching Data]]
- [[#📒 439. Exploring the Redux DevTools]]
- [[#📒 440. Summary]]

----
## 📒 427. Redux & Side Effects (and Asynchronous Code)
- Reducers must be **pure**, **side-effect free**, **synchronous functions**.
	- 순수함수
	- 부수효과 없음
	- 동기적
- Input (Old State + Action) --> Output (New State)
	- 리덕스의 리듀서와 useReducer 훅의 리듀서도 똑같이 작동합니다.
- Where should side-effects(부수효과가 있고) and async(비동기 코드들은 어디에 넣어야 하나요?) tasks be executed? 
	- Inside the components (e.g via `useEffect()`)
	- Inside the action creators
## 📒 428. Refresher / Practice: Part 1/2
[예제코드](https://codesandbox.io/s/advanced-redux-yu43d7)
### 🐿️ 함께 구현하기 전에 혼자 구현해보기
#### 요구사항
- [ ] `My Cart` 버튼을 눌렀을 때, 쇼핑카트 컴포넌트가 토글 (Show - Hide)
- [ ] `Add to Cart` 버튼을 눌렀을 때, 카트에 추가하기
	- [ ] 이미 카트에 추가되어있을 경우, 아이템의 양만 증가시키기
	- [ ] `-`, `+` 상호작용 - 수가 1일 경우 마이너스 버튼을 누르면 아이템을 쇼핑카드에서 제거
- [ ] Favorite Products 리스트에서 Dummy Products 를 더 추가해도 됨

1. 1차시도 -> `😭 실패 ㅠ`
2. 2차시도 -> 

https://redux-toolkit.js.org/tutorials/quick-start

- `initialState`에서 여러가지 값을 넣을 수 있는가?
----
### Redux 설치하기
`npm install @reduxjs/toolkit react-redux` 
### Redux store 폴더 만들기
- 이름이 꼭 store일 필요는 없지만, 디렉토리 이름을 store로 만드는 것이 컨벤션.
- `store` 폴더 아래에 `index.js` 파일 만들기. 
	- Redux store 를 셋업할 곳.

- `store` 폴더 아래에 cart-slice.js 와 ui-slice.js 파일 만들기
	- `cart-slice.js`: `Cart` 컴포넌트안의 값을 관리하는 slice 파일
	- `ui-slice.js`: `My Cart` 버튼을 눌렀을 때, `Cart` 컴포넌트가 토글되는 걸 관리하는 slice 파일
### ui-slice.js 와 index.js 셋업하기
**`store/ui-slice.js`**
```js
import { createSlice } from '@reduxjs/toolkit'

const uiSlice = createSlice({
    name: 'ui',
    initialState: {
        cartIsVisible: false
    },
    reducers: {
        toggle(state){
            // We are not really mutating the state now
            // Redux toolkit will capture this code
            // and use another third party library Immer to ensure
            // that this is actually translated to some immutable code
            // which creates a new state object instead of manipulating the existing one.
            state.cartIsVisible = !state.cartIsVisible
        }
    }
});

export const uiActions = uiSlice.actions;

export default uiSlice;
```

**`store/index.js`**
```js
import { configureStore } from '@reduxjs/toolkit';

import uiSlice from './ui-slice';

const store = configureStore({
    reducer: {
        ui: uiSlice.reducer
    }
})

export default store;
```

**`src/index.js`**
```js
import ReactDOM from 'react-dom/client'

import "./index.css";
import App from "./App";
import { store } from "./app/store";
import { Provider } from "react-redux";

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <Provider store={store}>
    <App />
  </Provider>,
);

```

**`src/components/Cart/CartButton.js`**
카트가 보였다가 숨겨졌다가를 토글링하기 위해서 CartButton 파일에 함수를 설정해주자
```js
import classes from "./CartButton.module.css";
import { uiActions } from "../../store/ui-slice";
import { useDispatch } from "react-redux";

const CartButton = () => {

  const dispatch = useDispatch()
  const toggleCartHandler = () => {
    dispatch(uiActions.toggle())
  };

  return (
    <button className={classes.button} onClick={toggleCartHandler}>
      <span>My Cart</span>
      <span className={classes.badge}>1</span>
    </button>
  );
};

export default CartButton;

```

**`App.js`**
```js
import React from "react";
import { useSelector } from "react-redux";
import Cart from "./components/Cart/Cart";
import Layout from "./components/Layout/Layout";
import Products from "./components/Shop/Products";

function App() {
 const showCart = useSelector((state) => state.ui.cartIsVisible);

  return (
    <Layout>
      {showCart && <Cart />}
      <Products />
    </Layout>
  );
}

export default App;

```

**`index.js`**
```js
import ReactDOM from 'react-dom/client'

import "./index.css";
import App from "./App";
import { Provider } from "react-redux";
import store from './store/index'

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <Provider store={store}>
    <App />
  </Provider>,
);
```

###  index.js 와 cart-slice.js 셋업하기

**`cart-slice.js`**
```js
import { createSlice } from '@reduxjs/toolkit'

createSlice({
    name: 'cart',
    initialState: {
        items: [],
        totalQuantity: 0,
    },
    reducers: {
        addItemToCart(state, action){
            const newItem = action.payload;
            const existingItem = state.items.find(item => item.id === newItem.id)
            if(!existingItem) {
                state.items.push({
                    itemId: newItem.id, price: newItem.price, quantity: 1, totalPrice: newItem.price, name: newItem.title
                });
            } else {
                existingItem.quantity++
                existingItem.totalPrice = existingItem.totalPrice + newItem.price;
            }
        },
        removeItemFromCart(){},
    }
})
```

## 📒 429. Refresher / Practice: Part 2/2
`store/cart-slice.js`
```js
import { createSlice } from '@reduxjs/toolkit'

const cartSlice = createSlice({
    name: 'cart',
    initialState: {
        items: [],
        totalQuantity: 0,
    },
    reducers: {
        addItemToCart(state, action){
            const newItem = action.payload;
            const existingItem = state.items.find(item => item.id === newItem.id)
            if(!existingItem) {
                state.items.push({
                    itemId: newItem.id, price: newItem.price, quantity: 1, totalPrice: newItem.price, name: newItem.title
                });
            } else {
                existingItem.quantity++
                existingItem.totalPrice = existingItem.totalPrice + newItem.price;
            }
        },
        removeItemFromCart(state, action){
            const id  = action.payload;
            const existingItem = state.items.find(item => item.id === id)
            if(existingItem.quantity === 1){
                state.items = state.items.filter(item => item.id !== id)
            } else {
                existingItem.quantity--;
               // existingItem.totalPrice = existingItem.totalPrice - existingItem.price;
            }
        },
    }
})

export const cartActions = cartSlice.actions;                 

export default cartSlice;
```

`src/store/index.js`
```js
import { configureStore } from '@reduxjs/toolkit';

import uiSlice from './ui-slice';
import cartSlice from './cart-slice'

const store = configureStore({
    reducer: {
        ui: uiSlice.reducer, cart: cartSlice.reducer
    }
})

export default store;
```

`components/Products.js`
```js
import ProductItem from "./ProductItem";
import classes from "./Products.module.css";

const DUMMY_PRODUCTS = [
  {
    id: "p1",
    price: 6,
    title: "My First Book",
    description: "My First book I ever wrote",
  },
  {
    id: "p2",
    price: 5,
    title: "My second Book",
    description: "My second book I ever wrote",
  },
];

const Products = (props) => {
  return (
    <section className={classes.products}>
      <h2>Buy your favorite products</h2>
      <ul>
        {DUMMY_PRODUCTS.map((product) => {
          <ProductItem
            key={product.id}
            title={product.title}
            price={product.price}
            description={product.description}
          />;
        })}
      </ul>
    </section>
  );
};

export default Products;

```

`src/components/ProductItem`
```js
import Card from "../UI/Card";
import classes from "./ProductItem.module.css";
import { cartActions } from "../../store/cart-slice";

const ProductItem = (props) => {
  const dispatch = useDispatch();
  const { title, price, description, id } = props;
  const addToCartHandler = () => {
    dispatch(
      cartActions.addItemToCart({
        id,
        title,
        price,
      }),
    );
  };

  return (
    <li className={classes.item}>
      <Card>
        <header>
          <h3>{title}</h3>
          <div className={classes.price}>${price.toFixed(2)}</div>
        </header>
        <p>{description}</p>
        <div className={classes.actions}>
          <button onClick={addToCartHandler}>Add to Cart</button>
        </div>
      </Card>
    </li>
  );
};

export default ProductItem;


```

`src/components/shop/Products.js`
```js
import ProductItem from "./ProductItem";
import classes from "./Products.module.css";

const DUMMY_PRODUCTS = [
  {
    id: "p1",
    price: 6,
    title: "My First Book",
    description: "My First book I ever wrote",
  },
  {
    id: "p2",
    price: 5,
    title: "My second Book",
    description: "My second book I ever wrote",
  },
];

const Products = () => {
  return (
    <section className={classes.products}>
      <h2>Buy your favorite products</h2>
      <ul>
        {DUMMY_PRODUCTS.map((product) => (
          <ProductItem
            key={product.id}
            id={product.id}
            title={product.title}
            price={product.price}
            description={product.description}
          />
        ))}
      </ul>
    </section>
  );
};

export default Products;
```

### 💭 궁금증들

- `components` 디렉토리 아래에 있는 `Cart`, `Layout`, `Shop`, `UI` 디렉토리들의 차이점은? 특히 `UI` 디렉토리의 목적은?![[Screenshot 2023-11-22 at 11.18.49.png]]
  - **`Layout 디렉토리`**: 
	  - 애플리케이션의 전체 구조나 레이아웃을 정의하는 컴포넌트.
  - **`UI 디렉토리`**: 
	  - 여러 곳에서 재사용 가능한 작은 UI 인터페이스 개별요소 컴포넌트.

[Practice - 01](https://codesandbox.io/p/devbox/advanced-redux-forked-3dc8g3?file=%2Fsrc%2Fstore%2Fcart-slice.js%3A25%2C8)

### [리덕스 툴킷 튜토리얼 살펴보기](https://redux-toolkit.js.org/tutorials/quick-start)
강의만 듣는 걸론 이해가 잘 안된다. 

1. `app/store.js` 파일을 생성하고 `configureStore` API를 사용하여 Redux 저장소를 만드세요.
   - 이 API는 Redux 저장소를 구성합니다.
   - Redux DevTools 확장 기능 사용을 가능하게 합니다.
2. `src/index.js` 파일에서 `Provider` 컴포넌트로 React 앱을 감싸고, 만들어진 Redux 저장소를 `store` 속성으로 전달해 React 컴포넌트에 Redux 저장소를 제공하세요.
   - `Provider` 컴포넌트는 React-Redux에 포함됩니다.
   - `<App>` 컴포넌트를 감싸는 데 사용됩니다.
3. `src/features/counter/counterSlice.js` 파일을 만들고 `createSlice` API를 사용하여 Redux "slice" 리듀서를 생성하세요.
   - `immer`를 사용하여 상태를 직접 변경하는 코드 작성이 가능합니다.
   - 생성된 슬라이스 리듀서와 액션 생성 함수들을 내보냅니다.
4. `counterSlice.js`에서 리듀서 함수를 가져와서 저장소의 `reducer` 매개변수에 추가함으로써 슬라이스 리듀서를 저장소에 추가하세요.
   - 이 리듀서는 해당 상태의 모든 업데이트를 처리합니다.
5. React 컴포넌트에서 Redux 상태와 액션을 사용하려면, `useSelector`와 `useDispatch` 훅을 사용하세요.
   - `useSelector`로 저장소에서 데이터를 읽습니다.
   - `useDispatch`로 액션을 발행합니다.
   - `src/features/counter/Counter.js` 파일을 생성하고 `<Counter>` 컴포넌트를 `App.js`에 렌더링하세요.
## 📒 430. Redux & Async Code
`Firebase` 를 사용해서 실시간 데이터베이스를 업데이트하자!

> [!question] 리듀서안에 HTTP 리퀘스트를 날려도 되나요?
> **NOPE**, 동기적 코드건 비동기적 코드건 리듀서 안에서 사이드 이펙트를 주어선 안된다.
> Reducers 는 반드시 순수함수, 사이드 이펙트 프리, 동기적 함수여야한다.
> `Input(Old State + Action) ---> Output(New State)`

> [!success] 그럼 어디에 넣을 수 있나요?
> 1. 컴포넌트 안에(e.g `useEffect()`)
> 2. `action creators` 안에

## 📒 431. Frontend Code vs Backend Code
**Server side code**? 
Allows you to **add your own code on the Firebase backend** which can triggered for incoming requests and which would allow you to transform data on the backend.
![[Screenshot 2023-11-23 at 14.29.40.png | 500]]
Frontend Code Depends On Backend Code

## 📒 432. Where To Put Our Logic

> [!question]- Where should side effects & async tasks be executed?
> 1. Inside the **components** (e.g. via `useEffect()`)
> 2. Inside the **action creators**

[Practice](https://codesandbox.io/p/devbox/432-where-to-put-our-logic-89zwk2?file=%2Fsrc%2Fstore%2Fcart-slice.js)


## 📒 433. Using useEffect with Redux

## 📒 434. A Problem with useEffect()
## 📒 435. Handling Http States & Feedback with Redux
## 📒 436. Using an Action Creator Thunk
## 📒 437. Finalizing the Fetching Logic

## 📒 438. Getting Started with Fetching Data
## 📒 439. Exploring the Redux DevTools
## 📒 440. Summary
