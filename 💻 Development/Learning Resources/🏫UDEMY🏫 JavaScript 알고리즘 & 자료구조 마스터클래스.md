 ```js
 function addUpTo(n) {
  return n * (n + 1) / 2;
}

var time1 = performance.now();
addUpTo(1000000000);
var time2 = performance.now();
console.log(`Time Elapsed: ${(time2 - time1) / 1000} seconds.`)
 ```
> O(1)
```js
function addUpTo(n) {
  let total = 0;
  for (let i = 1; i <= n; i++) {
    total += i;
  }
  return total;
}

var t1 = performance.now();
addUpTo(1000000000);
var t2 = performance.now();
console.log(`Time Elapsed: ${(t2 - t1) / 1000} seconds.`)
```
> O(n)
- n additions.
- n assignments.
- n comparisons.
---
- 코드 시간 재기
- `performance.now()` 함수
	- 수동으로 타이밍을 구하는 건 사실 좋은 방법은 아님.
	- 기기에 따라 다르게 측정된다.
- 덧셈공식

> [!faq] 수동으로 코드 시간재기가 좋은 방법이 아니면 뭐가 좋은 방법인가요?
> Counting Operations -> 연산 수 세기
> 정확한 수는 중요하지 않음. N이 커질 수록 비례적으로 커지는가? 가 중요.

> [!question] 그렇다면 중첩 for 문은 O(2n) 일까? NOPE
 O(n^2) 임. 제곱의 값으로 늘어나기 때문에 

**n이 커질 때 시간에 어떻게 영향을 받나요?**
## 상수는 중요하지 않다.
![[Screenshot 2023-12-13 at 11.18.29.png]]
