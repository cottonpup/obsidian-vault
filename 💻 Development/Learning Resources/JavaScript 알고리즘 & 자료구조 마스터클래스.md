****# 시간 복잡도
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

n이 커질 때 시간에 어떻게 영향을 받나요?
## 상수는 중요하지 않다.
![[Screenshot 2023-12-13 at 11.18.29.png]]
![[Screenshot 2023-12-13 at 11.20.26.png]]
![[Screenshot 2023-12-13 at 11.31.55.png]]
![[Screenshot 2023-12-13 at 11.36.20.png]]
`O(n^3)` 이 `O(n^2)` 보다 크니까 `O(n^2)` 를 무시

# 공간 복잡도
![[Screenshot 2023-12-13 at 11.49.51.png]]
# 로그와 섹션요약
![[Screenshot 2023-12-13 at 11.57.20.png]]
![[Screenshot 2023-12-13 at 11.57.46.png]]
# 빌트인 데이터 구조
![[Screenshot 2023-12-13 at 22.55.51.png]]
![[Screenshot 2023-12-13 at 22.56.09.png]]
![[Screenshot 2023-12-13 at 22.56.26.png]]
![[Screenshot 2023-12-13 at 22.56.40.png]]
# 객체 vs 배열
## When to use objects
- When you don't need order
- When you need fast access / insertion and removal
## # WHEN TO USE ARRAYS
- When you need order
- When you need fast access / insertion and removal (sort of....)

# 2단계 구체적 예제들
input과 output 이 없는 문제를 받으면 일단 스스로 인풋과 아웃풋을 적어볼 것.
```js
// Write a function which takes in a string and returns counts of each character in the string.

charCount("aaaa") // {a: 4}
charCount("hello") // 
```