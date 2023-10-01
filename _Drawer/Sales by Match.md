%%
[[Development]]
- [ ] 1차 복습 
- [ ] 2차 복습
- [ ] 3차 복습
%%
-----

>[!abstract] HackerRank 
>**Warm-up Challenges** - Sales by Match
> [Problem Link](https://www.hackerrank.com/challenges/sock-merchant/problem?h_l=interview&isFullScreen=true&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=warmup)
> ⏳ 1차 시도 -> 성공
> > [!check] 복습
> > - [ ] 1차 복습

### 문제 난이도
쉽지만 어떻게 풀어야할 지 잘 감이 안온다.

### 첫번째 솔루션
```js
function sockMerchant(n, socks) {
    const pairsList = {};
    let pairs = 0;
    socks.forEach(sock => {
        sock in pairsList ? pairsList[sock]++ : pairsList[sock] = 1;
    })
 
    Object.values(pairsList).forEach(item => {
        pairs = pairs + Math.floor(item / 2)
    })
    return pairs
}
```

### 두번째 솔루션
YouTube 에서 `Set` 메서드를 사용해서 문제를 푸는 법을 알려줬다. 왜 그걸 떠올리지 못했는지 조금 아쉽다. `Set`은 중복된 것을 다 지워주고 `has` 와 같은 메서드가 있다. 
```js
function sockMerchant(n, socks) {
    let pairs = 0;
    let search = new Set();
    for(const sock of socks) {
        if(search.has(sock)){
            pairs++;
            search.delete(sock)
        } else {
            search.add(sock)
        }
    } 
}
```

> [!faq] for...of 문이란? 
> - `for...of` - Use to loop over strings and arrays.
>	- iterates over values that the iterable object defines to be iterated over.
>		- each of their prototype objects implements an `@@iterator` method. So, for...of loop works on the mentioned object types.
>- `for...in` - Use to loop over objects.
> 	- iterates over the enumerable string properties of an object
>
>Object in JavaScript is not iterable by default. 
>So, `for...of` loop does not work on objects.
>  
>[for..of MDN Link](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)

