---
Created: 2023-10-23
tags:
---
# Resume.io 클론 프로젝트 분석하기
# App.tsx
- 전역으로 `isFullPreview` 라는 이름의 상태를 `useState`로 전체 화면 미리보기 기능을 관리합니다.
### 면접 스타일의 질문:
1. `isFullPreview` 상태는 어떤 목적으로 사용되나요? 이 상태가 변경될 때 어떤 동작을 기대하나요?
	유저의 뷰포인트 너비가 특정값 이하인 경우, EditorView만 보이게 설정하였습니다. 
2. `EditorView`와 `PagesView` 컴포넌트는 어떤 기능을 수행하나요?
	EditorView는 유저가 인풋을 입력하는 창이고, PagesView는 유저가 입력한 값을 토대로 나오는 프리뷰 창입니다. 
3. `useState` 외에 React의 어떤 훅을 사용해 본 경험이 있나요? 그리고 어떤 상황에서 사용하셨나요?
	`useEffect`훅을 사용해 본 경험이 있습니다. 특정 state가 업데이트 될 때마다 사이드 이펙트를 주고싶을 때 사용해본 경험이 있습니다. 
# App.test.tsx
코드는 React 애플리케이션의 `App` 컴포넌트를 테스트하기 위한 Jest와 Testing Library 테스트 스니펫입니다. `render` 함수를 사용하여 `App` 컴포넌트를 렌더링하고, `screen.getByText`를 사용하여 "learn react"라는 텍스트를 가진 엘리먼트를 찾습니다. 마지막으로 `expect`를 사용하여 해당 엘리먼트가 문서에 존재하는지 확인합니다.

### 면접 스타일의 질문

1. `@testing-library/react`를 사용하는 주요 이유는 무엇인가요? 왜 Jest와 함께 사용하나요?
2. `render` 함수는 어떤 역할을 하나요?
3. `screen.getByText`는 어떤 작업을 수행하고 어떤 값을 반환하나요?
4. `expect(linkElement).toBeInTheDocument();` 이 코드 라인이 의미하는 것은 무엇인가요?
5. 만약 테스트를 실패하게 만드는 변경사항이 생겼다면, 어떤 방법으로 디버깅을 하실 계획인가요?
6. 테스트 주도 개발(TDD)에 대한 의견을 들어볼 수 있을까요? 이 방법론을 적용해 본 경험이 있나요?
7. 어떤 컴포넌트나 기능을 테스트할 때, 어떤 기준으로 테스트 케이스를 작성하나요?
# ./src/state 
## /action-creators
## /action-types
## /actions
## /reducers
# ./src/Components
## /EditorView
## /PagesView
## /UI
## /hooks
---
# References
1. https://github.com/cottonpup/resume-builder