

for loop 보단 for of 문

```jsx
function charCount(str) {
    var obj = {};
    for (var char of str) {
        char = char.toLowerCase();
        if (/[a-z0-9]/.test(char)) {
            if (obj[char] > 0) {
                obj[char]++;
            } else {
                obj[char] = 1;
            }
        }
    }
    return obj;
}
```

```jsx
function charCount(str) {
    var obj = {};
    for (var char of str) {
        char = char.toLowerCase();
        if (/[a-z0-9]/.test(char)) {
            obj[char] = ++obj[char] || 1;
        }
    }
		return obj;
}
```

/[a-z0-9]/ 를 알 수 있을까?? 인터뷰 도중 말야...

매우 간단하긴 하다. 알파벳인지 숫자인지 체크.

하지만 만약 이 regular expression을 모른다면 더 좋은 방법이 있음.

`charCodeAt(0)` 를 사용할 수 있음.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5779800f-0715-4ebc-b24a-6accb0fdbb74/Untitled.png)

![심지어 더 빠르다..! 근데 어떻게 외움 ㅋㅋㅋㅋㅋ 뭐임..](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/09daf52b-4e75-4f82-97bc-9f0e2bf91be3/Untitled.png)

심지어 더 빠르다..! 근데 어떻게 외움 ㅋㅋㅋㅋㅋ 뭐임..

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cb4f4356-f609-4d18-8b6c-6a07e323a782/Untitled.png)

# Frequency Counters

Write a function called same, which accepts two arrays. The function should return true if every value in the array has it's corresponding value squared in the second array. The frequency of values must be the same.

```jsx
same([1,2,3], [4,1,9]) // true
same([1,2,3], [1,9]) // false
same([1,2,1], [4,4,1]) // false (must be same frequency)
```

- [x] Write a function called same
- [x] Accepts two arrays
- [x] firstArray 의 value loop 돌려서 확인.
- [ ] The function should return true if every value in the array has it's corresponding value squared in the second array
- [ ] The frequency of values must be the same

## A Naive Solution

```jsx
function same(arr1, arr2){
		// The frequency of values must be the same! 
    if(arr1.length !== arr2.length){
        return false;
    }

    for(let i = 0; i < arr1.length; i++){
        let correctIndex = arr2.indexOf(arr1[i] ** 2)
        if(correctIndex === -1) {
						// arr2 에 값이 존재하지 않으면 -1 
            return false;
        }
        arr2.splice(correctIndex,1) // If it is correct, then remove it from arr2
    }
    return true
}
```

`**Time Complexity - N^2` ⇒ nested loop**

indexOf 가 뭐더라..

[Array.prototype.indexOf() - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)

## Refactored Solution

```jsx
function same(arr1, arr2){
		// 5 !== 5 => false; => skip 
    if(arr1.length !== arr2.length){
        return false;
    }
		
    let frequencyCounter1 = {}
    let frequencyCounter2 = {}
    
		// loop arrays 
		for(let val of arr1){
        frequencyCounter1[val] = (frequencyCounter1[val] || 0) + 1
				// [1, 2, 3, 2, 5]
				// frequencyCoutner1[1] = (frequncyCounter1[1] || 0) + 1 
				// 프로퍼티가 없으면 1로 initialize 한다. 
			  // { 1: 1, 2: 2, 4: 1, 5: 1 }
	 }

    for(let val of arr2){
        frequencyCounter2[val] = (frequencyCounter2[val] || 0) + 1  
				// { 9: 1, 1: 1, 4: 2, 11: 1 }      
    }
    for(let key in frequencyCounter1){
				// frequnceyCounter 1 프로퍼티 loop
        if(!(key ** 2 in frequencyCounter2)){
					  // counter1의 프로퍼티를 square한 값이 Counter2에 있는 지 체크
						// { 1: 1, 2: 2, 3: 1, 5: 1 } => Coutner1
						// { 9: 1, 1: 1, 4: 2, 11: 1 } => Counter2 
						// 1 ** 2 => 1  (o)
						// 2 ** 2 => 4  (o)
						// 3 ** 2 => 9  (o)
						// 4 ** 2 => 16 (x)
            return false
        }

        if(frequencyCounter2[key ** 2] !== frequencyCounter1[key]){
            return false
        }
 
    }
    return true
}

same([1, 2, 3, 2, 5], [9, 1, 4, 4, 11]);
```

`Time Complexity - O(n)` ⇒ linear / without nested loop

## 빈 객체에 blanket notation으로 프로퍼티 접근

빈 객체에 bracket notation으로 프로퍼티를 접근하면 오류가 발생하는 것이 아니라, 객체에 따로 추가된다.

```jsx
let obj = {};
obj['first'] = 1;
obj['second'] = 2;
console.log(obj);
// {first: 1, second: 2}
```

## In operator 란

[in operator - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in)

```jsx
const car = { make: 'Honda', model: 'Accord', year: 1998 };

console.log('make' in car);
// expected output: true

delete car.make;
if ('make' in car === false) {
  car.make = 'Suzuki';
}

console.log(car.make);
// expected output: "Suzuki"
```

<aside> ❓ for of 와 for in의 차이가 뭐더라?

</aside>

<aside> ❓ object와 array의 차이가 뭐더라?

</aside>

# Anagrams

<aside> ❓ Edge cases? An edge case is a problem or situation that occurs only at an extreme operating parameter. For example, a stereo speaker might noticeably distort audio when played at maximum volume, even in the absence of any other extreme setting or condition. An edge case can be expected or unexpected.

</aside>

Given two strings, write a function to determine if the second string is an anagram of the first. An anagram is a word, phrase, or name formed by rearranging the letters of another, such as cinema, formed from iceman.

```jsx
validAnagram('', '') // true
validAnagram('aaz', 'zza') // false
validAnagram('anagram', 'nagaram') // true
validAnagram("rat","car") // false) // false
validAnagram('awesome', 'awesom') // false
validAnagram('qwerty', 'qeywrt') // true
validAnagram('texttwisttime', 'timetwisttext') // true
```

- [x] Write a function called validAnagram
- [x] Input ⇒ two strings
- [ ] Check If the second string is an anagram of the first
- [x] Make it lowercase, trim spaces

1. Loop strings ⇒ for .. of 문 활용가능

지금 안되는 것을 작게 적어보자.

Check If the second string is an anagram of the first

- [ ] delete specific string from input string.

first: {g: 1, e: 1, l: 2, o: 1}, second: {g: 1, e: 1, l: 2, o: 1}

string.replace('specific', '');

obj 에서 지워야 하지 않을까?,.....

시간이 너무 오래걸려 포기!