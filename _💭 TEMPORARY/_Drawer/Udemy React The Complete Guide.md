---
Date: 2023-07-07
Tags: React, Udemy/React, Udemy
---
%%[[Development]]%%

```dataview 
TABLE without ID
	file.link.alias as "제목",
	date as "날짜"
FROM #Udemy/React/SubPost 
```

--------
# Review

### [리덕스 공식페이지 - 리덕스 핵심](https://redux.js.org/tutorials/essentials/part-1-overview-concepts)
- Actions
	- Action은 type 필드가 있는 순수한 자바스크립트 객체이다. 액션은 어플리케이션에서 일어난 일을 설명하는 이벤트이다.
		- type 필드에는 `todos/todoAdded` 와 같이 `domain/eventName` 형식을 갖춘 서술적인 문자열 이름이 있어야 합니다.  
		- 액션 객체에는 추가 정보를 전달하는 `payload`라는 다른 필드도 가집니다.
- Action Creators
	- 액션 객체를 만들고 리턴하는 함수입니다. 
		- 액션 크리에이터 함수를 통해서 우리는 매번 액션 객체를 손으로 적지 않아도 되는 장점이 있습니다.
- Reducers
	- 현재 `state`와 `action`객체를 받고 `state`를 어떻게 업데이트하는지 결정하거나 새로운 `state`를 리턴하는 함수입니다.
	- 리듀서는 액션 타입의 이벤트를 다루는 이벤트 리스너와 비슷합니다. 
		- 리듀서는 절대 `state`를 조작해서는 안되고 불변의 업데이트만 가능합니다.
		- 리듀서는 절대 비동기 로직을 사용하거나 랜덤한 값을 계산하거나 사이드 이펙트를 발생시키는 일을 해서는 안됩니다.
		- 리듀서는 액션이 발생하면 이전 상태 값의 사본을 만들고, 새로운 상태 값으로 그 사본을 업데이트를 합니다. 만약 액션 객체를 받지 않으면 이전 상태 값 그대로 리턴합니다.
- Store
	- 리덕스의 상태값을 갖는 객체입니다. 
	- 리듀서를 실행시켜 스토어를 생성하고 현재 상태 값을 리턴하는 `getState` 라는 메서드를 가지고 있습니다.
- Dispatch
	- 상태 값을 업데이트하기 위해 `store.dispatch()`를 호출하고 액션 객체를 전달하는 메서드입니다.
- Selectors
	- 스토어 상태 값에서 특정한 정보값을 끌어오는 함수입니다.

### [리덕스 툴킷 앱 구조](https://redux.js.org/tutorials/essentials/part-2-app-structure)
createSlice
configureStore
Redux Toolkit allows us to write "mutating" logic in reducers.


----
Redux 직접 복습해보기
1. `src/app/store/js` 파일 생성하기
2. configureStore
![[Screenshot 2023-07-12 at 10.36.49 PM.png]]
----
# 리덕스 Q&A

![[Screenshot 2023-07-17 at 9.51.59 PM.png]]

![[Screenshot 2023-07-17 at 10.18.07 PM.png]]

> [!faq] What is Fragment? And why should I use it? And why can't I insert just an element?
> 리액트에서는 하나의 컴포넌트가 여러 개의 엘리먼트들을 반환한다. 리액트를 사용하기 위한 문법인 JSX 를 쓸 때, return 문 안에는 반드시 하나의 최상위 태그가 있어야 한다. 이는 리액트가 하나의 컴포넌트만을 리턴할 수 있기 때문이다.
> 의미없는 div 를 반환하지 않아도 된다.

