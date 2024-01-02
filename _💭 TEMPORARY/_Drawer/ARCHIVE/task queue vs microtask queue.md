- **태스크 큐**
	- Task Queue는 Web API가 수행한 비동기 함수를 넘겨받아 Event Loop가 해당 함수를 Call Stack에 넘겨줄 때까지 비동기 함수들을 쌓아놓는 곳이다.
	- setTimeOut()
- **마이크로 태스크 큐**
	-  마이크로 태스크 큐는 Promise나 async/await, process.nextTick, Object.observe, MutationObserver과 같은 비동기 호출을 넘겨받는다.
# References
- https://velog.io/@titu/JavaScript-Task-Queue%EB%A7%90%EA%B3%A0-%EB%8B%A4%EB%A5%B8-%ED%81%90%EA%B0%80-%EB%8D%94-%EC%9E%88%EB%8B%A4%EA%B3%A0-MicroTask-Queue-Animation-Frames-Render-Queue