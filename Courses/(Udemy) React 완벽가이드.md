# Section 20: Advanced Redux
## 427. Redux & Side Effects (and Asynchronous Code)
- Reducers must be **pure**, **side-effect free**, **synchronous functions**.
	- 순수함수
	- 부수효과 없음
	- 동기적
- Input (Old State + Action) --> Output (New State)
	- 리덕스의 리듀서와 useReducer 훅의 리듀서도 똑같이 작동합니다.
- Where should side-effects(부수효과가 있고) and async(비동기 코드들은 어디에 넣어야 하나요?) tasks be executed? 
	- Inside the components (e.g via `useEffect()`)
	- Inside the action creators
## 428. Refresher / Practice: Part 1/2
[예제코드](https://codesandbox.io/s/advanced-redux-yu43d7)
[Forked 예제코드](https://codesandbox.io/s/advanced-redux-forked-jftfqs?file=/src/App.js)
### 함께 구현하기 전에 혼자 구현해보기
#### 요구사항
-[]
# Section 21: Building a Multi-Page SPA with React Router