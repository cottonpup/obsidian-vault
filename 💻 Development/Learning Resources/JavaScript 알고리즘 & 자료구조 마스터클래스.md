시간 복잡도
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

## 공간 복잡도
![[Screenshot 2023-12-13 at 11.49.51.png]]
## 로그와 섹션요약
![[Screenshot 2023-12-13 at 11.57.20.png]]
![[Screenshot 2023-12-13 at 11.57.46.png]]
## 빌트인 데이터 구조
![[Screenshot 2023-12-13 at 22.55.51.png]]
![[Screenshot 2023-12-13 at 22.56.09.png]]
![[Screenshot 2023-12-13 at 22.56.26.png]]
![[Screenshot 2023-12-13 at 22.56.40.png]]
## 객체 vs 배열
### When to use objects
- When you don't need order
- When you need fast access / insertion and removal
### # WHEN TO USE ARRAYS
- When you need order
- When you need fast access / insertion and removal (sort of....)

## 2단계 구체적 예제들
input과 output 이 없는 문제를 받으면 일단 스스로 인풋과 아웃풋을 적어볼 것.
```js
// Write a function which takes in a string and returns counts of each character in the string.

// 1️⃣ 일단 함수명을 적고 인풋을 가정, 아웃풋의 데이터 형태를 생각하고 아웃풋을 가정
charCount("aaaa") // {a: 4}
charCount("hello") // {h: 1, e: 1, l: 2, o: 1}

// 2️⃣ 복잡한 입력값과 예시를 알아봄.
"my phone number is 41242" // number?
"Hello hi" // 대소문자?
"" // 빈 인풋?
null // invalid 인풋?
```

## 3단계 세부 분석
- 세부화시키기 (Break it down)
	- 면접관들이 여러분이 수행하는 작업이 무엇인지에 대해 소통하기를 원함!
	- 미간을 찌푸린 채 말없이 바로 코드를 입력하지 마세요...
	- 여기서 이런 작업을 할거다! 라고 말하세요.
	- 주석으로 프레임을 적어놓으면 문제를 다 풀지 못해도 면접관이 생각의 흐름을 읽을 수 있습니다. 
## 4단계 해결 또는 단순화

## 5단계 되돌아보기와 리펙터
`/a-z0-9/.test(char)`: 정규 표현식을 사용하여 특수문자를 제외한 소문자, 숫자인지 확인하게 적음
- 하지만 정규표현식이 효율적인지는 확신이 안섭니다.
- 다른 방식이 있을까요? 문자코드를 알 수 있는 `charCodeAt(0)` 을 사용해봅시다.
- 정규 표현식보다 빠릅니다.
## 복습
- 문제를 이해하기
- 구체적인 예시를 살펴보기
- 세분화 하기
- 해결하기 / 단순화하기
- 되돌아보고 리팩토링하기

# 섹션 5: 문제 해결 패턴
# 섹션 6: 100% 선택적 도전 과제
# 섹션 7: 재귀
# 섹션 8: 재귀 문제 집합
# 섹션 9: 
