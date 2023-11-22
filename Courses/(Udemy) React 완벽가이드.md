# 💻 Section 20: Advanced Redux
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
[Forked 예제코드](https://codesandbox.io/s/advanced-redux-forked-jftfqs?file=/src/App.js)
### 🐿️ 함께 구현하기 전에 혼자 구현해보기
#### 요구사항
- [ ] `My Cart` 버튼을 눌렀을 때, 쇼핑카트 컴포넌트가 토글 (Show - Hide)
- [ ] `Add to Cart` 버튼을 눌렀을 때, 카트에 추가하기
	- [ ] 이미 카트에 추가되어있을 경우, 아이템의 양만 증가시키기
	- [ ] `-`, `+` 상호작용 - 수가 1일 경우 마이너스 버튼을 누르면 아이템을 쇼핑카드에서 제거
- [ ] Favorite Products 리스트에서 Dummy Products 를 더 추가해도 됨

`😭 실패 ㅠ `

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

## 📒 428. Refresher / Practice: Part 2/2
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
1. Redux Store 만들기
   `app/store.js` 파일을 만들어서 `configureStore` API를 임포트해준다.
   - Redux Store 형성.
   - Redux DevTools extension 을 사용하게 해준다.
2. Redux Store를 React에 제공하기
   `src/index.js`에서 앱을 React-Redux의 `<Provider>`로 감싸준다. 방금 만든 Redux Store를 임포트해서, `<App>`을 감싼 `<Provider>`에  , and pass the store as a prop
3. 

## 430. Redux & Async Code



# Section 21: Building a Multi-Page SPA with React Router
