
> [!note] What is *Redux*?
>A state management system for cross-component or app-wide state.

## #260
- Local State -> useState() / useReducer()
	- State that belongs to a single component 
	  E.G. Listening to user input in a input field. 
	  Toggling a "show more.." details field.
- Cross-Component State -> props chains / prop drilling
	- State that affects multiple components
- App-wide State -> props chains / prop drilling

## #261
React Context - Potential Disadvantages(Downsides)
- Complex Setup / Management
	- In more complex apps, managing React Context can lead to deeply nested JSX code and / or huge "Context Provider" components. 
- Performance
	- React Context is not optimized for high-frequency state changes

## #262
Components dispatch actions, which describe what should be done but don't manipulate it directly. Then these actions are forwarded to the reducer, the reducer does what the action wants.

## #264
- 빈 프로젝트 파일에 자바스크립트 파일 생성후, 터미널에서 `npm init -y` 실행하기
	- `-y` 가 모든 설정 질문에 'yes'를 디폴트로 생성한다.
- `npm install redux` 실행
- 생성한 자바스크립트 파일에 코드 내용을 추가한다

```js
const redux = require('redux');

// reducer function receives state and action by default
// and return new state.
  const counterReducer = (state, action) => {
	  return {
	  // existing value 
		  counter: state.counter + 1
	  };
  };

// we didn't execute `counterReducer`, `counterSubscriber`
// because both the reducer, as well as the subscriber function will be executed by Redux
  const store = redux.createStore(counterReducer);

  const counterSubscriber = () => {
  // getState is a method which is available on the store created with createStore
	  const latestState = store.getState();
	  console.log(latestState)
  }

  store.subscribe(counterSubscriber);
```
  
  - Run `node redux-demo.js` then throw an error.
	  - State를 처음 실행하는 거라 state의 fallback default value가 필요함.
	  - `(state = { counter: 0 }, action)` 이렇게 Reducer 함수에 값을 지정해준다.
- 그러나, console에 아무것도 찍히지 않는다. 액션을 dispatch 해주지 않아서 아무 일도 일어나지 않는 것이다. 따라서 아래와 같이 자바스크립 파일에 코드를 변경해준다.
  ```js
  const redux = require('redux');

  const counterReducer = (state = { counter: 0 }, action) => {
	  return {
		  counter: state.counter + 1
	  };
  };

  const store = redux.createStore(counterReducer);

  const counterSubscriber = () => {
	  const latestState = store.getState();
	  console.log(latestState)
  }

  store.subscribe(counterSubscriber);
  
  store.dispatch({ type: 'increment' })
  
  ```

## #265
Reducer 함수에서 이제 action의 type 을 통해 조건문을 만들 수 있다. 
  ```js
  const redux = require('redux');

  const counterReducer = (state = { counter: 0 }, action) => {
	  if (action.type === 'increment'){
		  return {
			  counter: state.counter + 1
		  }
		}

	  if (action.type === 'decrement'){
		  return {
			  counter: state.counter - 1
		  }
		}
		
	return state;
	  
  };

  const store = redux.createStore(counterReducer);

  const counterSubscriber = () => {
	  const latestState = store.getState();
	  console.log(latestState)
  }

  store.subscribe(counterSubscriber);
  
  store.dispatch({ type: 'increment' })
  store.dispatch({ type: 'decrement' })
  
  ```

## #266
npm install, n
npm start

## #267
store 디렉토리를 따로 생성하여 index.js 파일을 만든다. 그 이후, 이전에는 파일 안에서 바로 subscribe 했지만 이번에는 따로 컴포넌트에서 subscribe 할 수 있게 할 것이다. 따라서 export default 를 통해서 store 를 제공해주자. 
We need only one store. Then what does provide mean?

```js
import { createStore } from 'redux';

const counterReducer = (state = { counter: 0 }, action) => {
    if (action.type === 'increment') {
        state.counter += 1;
    }
    if (action.type === 'decrement') {
        state.counter -= 1;
    }

    return state;
};

const store = createStore(counterReducer);

export default store;

```

## #268
react-redux에서의 Provider 를 통해 subscribe 가 가능하다.
```js
import React from 'react';
import ReactDOM from 'react-dom/client';
import { Provider } from 'react-redux';

import './index.css';
import App from './App';
// `export default` 키워드를 통해서 받아올 때는 굳이 {} 로 묶어서 받아 올 필요가 없다.
import store from './store/index';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
    <Provider store={store}>
        <App />
    </Provider>,
);

```

## #269
> [!faq] What does `useSelector` do?
> It manages the subscription for you behind the scenes. 

When you use `useSelector`, React Redux will automatically set up a subscription to use the Redux store for this component. 

## #270
```js components/Counter.js
import { useSelector, useDispatch } from 'react-redux';
import classes from './Counter.module.css';

const Counter = () => {
    const dispatch = useDispatch();
    const counter = useSelector((state) => state.counter);

    const icrementHandler = () => {
        dispatch({ type: 'increment' });
    };
    const decrementHandler = () => {
        dispatch({ type: 'decrement' });
    };
    const toggleCounterHandler = () => {};

    return (
        <main className={classes.counter}>
            <h1>Redux Counter</h1>
            <div className={classes.value}>{counter}</div>
            <div>
                <button onClick={icrementHandler}>Increment</button>
                <button onClick={decrementHandler}>Decrement</button>
            </div>
            <button onClick={toggleCounterHandler}>Toggle Counter</button>
        </main>
    );
};

export default Counter;

```

### 트러블 슈팅
액션이 제대로 dispatch 되지 않았는데, 이유는 객체를 return 해야하는데 값을 지정했기 때문이다. 
```js store/index.js
import { createStore } from 'redux';

const counterReducer = (state = { counter: 0 }, action) => {
    if (action.type === 'increment') {
        return {
            counter: state.counter + 1,
        };
    }
    if (action.type === 'decrement') {
        return {
            counter: state.counter - 1,
        };
    }

    return state;
};

const store = createStore(counterReducer);

export default store;

```
## #271 Class-based Components with Rudux
class-based component 로 적어보기

```js
import { Component } from 'react';
import { connect } from 'react-redux';
import classes from './Counter.module.css';

class Counter extends Component {
    icrementHandler() {
        this.props.increment();
    }

    decrementHandler() {
        this.props.decrement();
    }

    toggleCounterHandler() {}

    render() {
        return (
            <main className={classes.counter}>
                <h1>Redux Counter</h1>
                <div className={classes.value}>{this.props.counter}</div>
                <div>
                    <button onClick={this.icrementHandler.bind(this)}>Increment</button>
                    <button onClick={this.decrementHandler.bind(this)}>Decrement</button>
                </div>
                <button onClick={this.toggleCounterHandler}>Toggle Counter</button>
            </main>
        );
    }
}

const mapStateToProps = (state) => {
    return {
        counter: state.counter,
    };
};

const mapDispatchToProps = (dispatch) => {
    return {
        increment: () =>
            dispatch({
                type: 'increment',
            }),
        decrement: () =>
            dispatch({
                type: 'decrement',
            }),
    };
};

export default connect(mapStateToProps, mapDispatchToProps)(Counter);

```
## #272
dispatch되는 payload 값에 amount 를 추가해놓자.
```js components/Counter.js
import { useSelector, useDispatch } from 'react-redux';
import classes from './Counter.module.css';

const Counter = () => {
    const dispatch = useDispatch();
    const counter = useSelector((state) => state.counter);

    const icrementHandler = () => {
        dispatch({ type: 'increment' });
    };
    const icreaseHandler = () => {
        dispatch({ type: 'increase', amount: 5 });
    };
    const decrementHandler = () => {
        dispatch({ type: 'decrement' });
    };
    const toggleCounterHandler = () => {};

    return (
        <main className={classes.counter}>
            <h1>Redux Counter</h1>
            <div className={classes.value}>{counter}</div>
            <div>
                <button onClick={icrementHandler}>Increment</button>
                <button onClick={icreaseHandler}>Increase by 5</button>
                <button onClick={decrementHandler}>Decrement</button>
            </div>
            <button onClick={toggleCounterHandler}>Toggle Counter</button>
        </main>
    );
};

export default Counter;

```
## #273
```js
import { useSelector, useDispatch } from 'react-redux';
import classes from './Counter.module.css';

const Counter = () => {
    const dispatch = useDispatch();
    const counter = useSelector((state) => state.counter);
    const show = useSelector((state) => state.showCounter);

    const icrementHandler = () => {
        dispatch({ type: 'increment' });
    };
    const icreaseHandler = () => {
        dispatch({ type: 'increase', amount: 5 });
    };
    const decrementHandler = () => {
        dispatch({ type: 'decrement' });
    };
    const toggleCounterHandler = () => {
        dispatch({ type: 'toggle' });
    };

    return (
        <main className={classes.counter}>
            <h1>Redux Counter</h1>
            {show && <div className={classes.value}>{counter}</div>}
            <div>
                <button onClick={icrementHandler}>Increment</button>
                <button onClick={icreaseHandler}>Increase by 5</button>
                <button onClick={decrementHandler}>Decrement</button>
            </div>
            <button onClick={toggleCounterHandler}>Toggle Counter</button>
        </main>
    );
};

export default Counter;
```
## #274
https://academind.com/tutorials/reference-vs-primitive-values/
### Primitive Values vs Reference Values
```js
    if (action.type === 'increment') {
        state.counter++;
        return state;
    }
```
^ 왜 위에가 틀릴까?
You should never change the existing state. always override it by returnning a brand new object.
Alwyas copy and create new objects 
## #275
프로젝트가 커짐에 따라 Indetifier 에 오타가 발생할 수 있다. 그러면 업데이트해야하는 state가 너무 많이 늘어나게 된다. 상수로 값을 지정해서 export로 변수를 보내주고 상수값을 사용하면 되겠지만, 이제는 대신 `Redux Tookit`을 사용할 수 있다. 
리덕스 툴킷은 리덕스를 더 쉽게 사용할 수 있게해준다. 
## #276
`npm install @reduxjs/toolkit` 으로 Redux Toolkit 설치하기. Redux Toolkit 안에 Redux가 이미 포함되어있기에 리덕스는 uninstall 해도 된다. 
Redux toolkit internally uses another package called Immer, which will detect code like this.

원래 리덕스에서는 리듀서 함수를 직접 상태를 변경하면 안되지만, Redux toolkit은 그것을 가능하게 하는데, 그 이유는 createReducer API가 내부적으로 자동으로 immer를 사용하기 때문에 괜찮다. 

https://redux-toolkit.js.org/usage/immer-reducers

```js
createSlice({
    name: 'counter',
    initialState,
    reducers: {
        increment(state) {
            state.counter++;
        },
        decremenet(state) {
            state.counter--;
        },
        increase(state, action) {
            state.counter = state.counter + action.amount;
        },
        toggleCounter(state) {
            state.showCounter = !state.showCounter;
        },
    },
});
```

## #277
`createStore`는 `configureStore`는 대체가능
`configureStore`는 지금까지의 `reducers`들을 `merge`해준다.
```js
import { createSlice, configureStore } from '@reduxjs/toolkit';

const initialState = { counter: 0, showCounter: true };

const counterSlice = createSlice({
    name: 'counter',
    initialState,
    reducers: {
        increment(state) {
            state.counter++;
        },
        decremenet(state) {
            state.counter--;
        },
        increase(state, action) {
            state.counter = state.counter + action.amount;
        },
        toggleCounter(state) {
            state.showCounter = !state.showCounter;
        },
    },
});

const store = configureStore({
    reducer: counterSlice.reducer,
});

export default store;

```

## #278
```js store/index.js
import { createSlice, configureStore } from '@reduxjs/toolkit';

const initialState = { counter: 0, showCounter: true };

const counterSlice = createSlice({
    name: 'counter',
    initialState,
    reducers: {
        increment(state) {
            state.counter++;
        },
        decremenet(state) {
            state.counter--;
        },
        increase(state, action) {
            // counterActions 에서 payload 를 받아온다.
            state.counter = state.counter + action.payload;
        },
        toggleCounter(state) {
            state.showCounter = !state.showCounter;
        },
    },
});

// `counterSlice.actions.toggleCounter;`
// Returns an action object of this shape
// {type: blabla}
// This will crate action objects

const store = configureStore({
    reducer: counterSlice.reducer,
});

export const counterActions = counterSlice.actions;

export default store;
```

```js components/Counter.js
import { useSelector, useDispatch } from 'react-redux';

import { counterActions } from '../store/index';
import classes from './Counter.module.css';

const Counter = () => {
    const dispatch = useDispatch();
    const counter = useSelector((state) => state.counter);
    const show = useSelector((state) => state.showCounter);

    const icrementHandler = () => {
        dispatch(counterActions.increment());
    };
    const icreaseHandler = () => {
        dispatch(counterActions.increase(5)); // { type: SOME_UNIQUE_IDENTIFER, payload: 10 }
    };
    const decrementHandler = () => {
        dispatch(counterActions.decremenet());
    };
    const toggleCounterHandler = () => {
        dispatch(counterActions.toggleCounter());
    };

    return (
        <main className={classes.counter}>
            <h1>Redux Counter</h1>
            {show && <div className={classes.value}>{counter}</div>}
            <div>
                <button onClick={icrementHandler}>Increment</button>
                <button onClick={icreaseHandler}>Increase by 5</button>
                <button onClick={decrementHandler}>Decrement</button>
            </div>
            <button onClick={toggleCounterHandler}>Toggle Counter</button>
        </main>
    );
};

export default Counter;
```

## #279
다수의 state를 다룰 때는 `creatSlice` 를 통해서 slice를 다시 만들어줄 수 있다.
```js
import { createSlice, configureStore } from '@reduxjs/toolkit';

const initialCounterState = { counter: 0, showCounter: true };

const counterSlice = createSlice({
    name: 'counter',
    initialState: initialCounterState,
    reducers: {
        increment(state) {
            state.counter++;
        },
        decremenet(state) {
            state.counter--;
        },
        increase(state, action) {
            state.counter = state.counter + action.payload;
        },
        toggleCounter(state) {
            state.showCounter = !state.showCounter;
        },
    },
});
const initialAuthState = { isAuthenticated: false };
const authSlice = createSlice({
    name: 'authentication',
    initialState: initialAuthState,
    reducers: {
        login(state) {
            state.isAuthenticated = true;
        },
        logout(state) {
            state.isAuthenticated = false;
        },
    },
});

// this will atuomatically be merged together into one main reducer
const store = configureStore({
    reducer: { counter: counterSlice.reducer, auth: authSlice.reducer },
});

export const counterActions = counterSlice.actions;
export const authActions = authSlice.actions;

export default store;
```

```js
import { useSelector, useDispatch } from 'react-redux';

import { counterActions } from '../store/index';
import classes from './Counter.module.css';

const Counter = () => {
    const dispatch = useDispatch();
    const counter = useSelector((state) => state.counter.counter);
    const show = useSelector((state) => state.counter.showCounter);

    const icrementHandler = () => {
        dispatch(counterActions.increment());
    };
    const icreaseHandler = () => {
        dispatch(counterActions.increase(5)); // { type: SOME_UNIQUE_IDENTIFER, payload: 10 }
    };
    const decrementHandler = () => {
        dispatch(counterActions.decremenet());
    };
    const toggleCounterHandler = () => {
        dispatch(counterActions.toggleCounter());
    };

    return (
        <main className={classes.counter}>
            <h1>Redux Counter</h1>
            {show && <div className={classes.value}>{counter}</div>}
            <div>
                <button onClick={icrementHandler}>Increment</button>
                <button onClick={icreaseHandler}>Increase by 5</button>
                <button onClick={decrementHandler}>Decrement</button>
            </div>
            <button onClick={toggleCounterHandler}>Toggle Counter</button>
        </main>
    );
};

export default Counter;
```

## #280

> [!faq] What is useSelector?
>  Allowing a selector function.

항상 한개의 Redux store 와 다양한 다른 state slices 가 필요하다.

## #281

## #282
![[Screenshot 2023-07-05 at 12.10.11 AM.png]]

![[Screenshot 2023-07-04 at 11.58.59 PM.png]]
