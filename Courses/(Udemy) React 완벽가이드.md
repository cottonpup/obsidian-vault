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
- [ ] `My Cart` 버튼을 눌렀을 때, 쇼핑카트 컴포넌트가 토글 (Show - Hide)
- [ ] `Add to Cart` 버튼을 눌렀을 때, 카트에 추가하기
	- [ ] 이미 카트에 추가되어있을 경우, 아이템의 양만 증가시키기
	- [ ] `-`, `+` 상호작용 - 수가 1일 경우 마이너스 버튼을 누르면 아이템을 쇼핑카드에서 제거
- [ ] Favorite Products 리스트에서 Dummy Products 를 더 추가해도 됨

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
### 
# Section 21: Building a Multi-Page SPA with React Router
