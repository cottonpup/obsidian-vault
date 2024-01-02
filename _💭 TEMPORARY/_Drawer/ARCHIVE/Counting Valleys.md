---
Date: 2023-07-07
Tags: Algorithm, CodingTest, Platform/Hackerrank
Platform: Hackerrank
Difficulty: Easy
Review: 0
---
%%
[[Development]]
- [ ] 1차 복습 
- [ ] 2차 복습
- [ ] 3차 복습
%%
> [!abstract] HackerRank 
> **Warm-up Challenges** - Counting Valleys
> ----
> [Problem Link](https://www.hackerrank.com/challenges/counting-valleys/problem?h_l=interview&isFullScreen=false&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=warmup)
> ⏳ 1차 시도 -> 포기
> ⏳ 2차 시도 -> 성공

### 문제 난이도
그렇게 어렵지 않은 문제임에도 불구하고 생각보다 코드를 구현하는데 있어서 어려웠다.

### 실패한 솔루션
일부 Test 코드는 통과했지만, 실제 코드를 실행했을 때는 실패했다. 문제를 잘 이해하지 못해서 발생한 일인데, 너무 복잡하게 생각했다. 골짜기에 내려갔다가 도로 Sea level 로 돌아온 횟수를 구하는 것이다. 
```js
function countingValleys(steps, path) {
    // Write your code here
    const records = [...path]
    let level = 0;
    let valleys = 0;
    records.forEach((currentPath, i)=> {
        if (currentPath === 'U'){
            level += 1
        } 
        if(currentPath === 'D'){
            level -= 1
        }
        
        if (level >= 0){
            if(currentPath === 'U' && records[i + 1] === 'D'){
                valleys += 1;
            }
        }
    })
    
    return valleys
}
```

### 두번째 솔루션
문제를 이해하고 얼마나 쉬운 문젠지 좀 알게됐다. 영어문제인건지.. 문제 파악 능력이 좀 많이 떨어지는 듯하다. 
```js
function countingValleys(steps, path) {
    // Write your code here
    let currentLevel = 0;
    let valleys = 0;
    for(let i = 0; i < steps; i++){
       if(path[i] === 'U'){
           currentLevel++
       } else {
           if(currentLevel === 0){
               valleys++
           }
           currentLevel--
       }
    }
    return valleys
}
```
