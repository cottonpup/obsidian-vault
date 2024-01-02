---
Date: 2023-07-16
Tags: Algorithm, CodingTest, Platform/Hackerrank
Platform: Hackerrank
Difficulty: Easy
Review: 0
---

```js
function jumpingOnClouds(c) {
    // Write your code here
    let jumps = 0;
    
    for(let i = 0; i <= c.length; i++){
        
        if(c[i] === 0){
            if(i !== 0){
                jumps += 1
            }
            if(c[i + 2] === 0){
                // i += 2 가 아닌데 왜 일까?
                // for 문이 돌아가기 전에 i를 임의로 변경하면 그 변경한 인덱스에서 코드가 돌아가는게 아니고 변경된 인덱스를 스킵하고 
                // 그 인덱스에서 for loop 을 마치고 1이 증가한다.  
                i += 1
            } 
        }
    }
    return jumps
}
```