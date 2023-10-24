---
Created: 2023-10-23
tags:
---
# Resume.io 클론 프로젝트 분석하기
# App.tsx
- 전역으로 `isFullPreview` 라는 이름의 상태를 `useState`로 전체 화면 미리보기 기능을 관리합니다.
### 면접 스타일의 질문:
1. `isFullPreview` 상태는 어떤 목적으로 사용되나요? 이 상태가 변경될 때 어떤 동작을 기대하나요?
	유저의 뷰포인트 너비가 특정값을 
2. `EditorView`와 `PagesView` 컴포넌트는 어떤 기능을 수행하나요?
	EditorView는 유저가 인풋을 입력하는 창이고, PagesView는 유저가 입력한 값을 토대로 나오는 프리뷰 창입니다. 
3. `useState` 외에 React의 어떤 훅을 사용해 본 경험이 있나요? 그리고 어떤 상황에서 사용하셨나요?
	`useEffect`훅을 사용해 본 경험이 있습니다. 특정 state가 업데이트 될 때마다 사이드 이펙트를 주고싶을 때 사용해본 경험이 있습니다. 
# App.test.tsx

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