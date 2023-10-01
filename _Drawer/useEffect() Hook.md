useEffect 함수란 리액트 컴포넌트가 랜더링 될 때마다 특정 작업을 실행할 수 있도록 하는 Hook 이다.

# useEffect() 하는 것?
렌더링 후에 무언가를 실행 하라고 말해주는 훅! DOM 업데이트 이후에 우리가 넘겨준 함수를 실행합니다. 
**Does `useEffect` run after every render?** Yes! By default, it runs both after the first render _and_ after every update.

--- 

리액트 공식문서에서는 라이프사이클 메서드보다 useEffect()훅을 사용해서[ 중복코드를 줄일 수 있다](https://legacy.reactjs.org/docs/hooks-effect.html#example-using-classes)고 한다. render 메서드는 부수 효과(Side effect)를 일으키지 못한다. 그래서 라이프 사이클에 `componentDidMount` 와 `componentDidUpdate`가 존재한다.

매번 렌더될 때 마다 Mount 가 되든 Update 가 되든 같은 부수 효과(Side effect)를 실행하게 하는 훅.

----
기존 상태를 참조하는 dependency 의존성이 생기면 Array에 넣어줘야 한다.

