# Section 20: Advanced Redux
## 295. 리덕스 및 부작용(및 비동기 코드)
- Reducers must be pure, side-effect, free, synchronous functions.
- Input (Old State + Action) --> Output (New State)
- Where should side-effects and async tasks be executed?
	- Inside the components (e.g `useEffect()`)
	- Inside the action creators

# Section 21: Building a Multi-Page SPA with React Router