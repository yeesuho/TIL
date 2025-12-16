2025.06.23

### ``push()``: 배열의 끝에 요소를 추가
```js
let fruits = ['apple', 'banana'];
fruits.push('orange');

console.log(fruits);  // ['apple', 'banana', 'orange']
```
- 'orange'가 배열의 뒤쪽에 추가됨

- 반환값은 추가된 후 배열의 길이

### ``pop()``: 배열의 끝 요소를 제거
```js
let fruits = ['apple', 'banana', 'orange'];
let last = fruits.pop();

console.log(fruits);  // ['apple', 'banana']
console.log(last);    // 'orange'
```
- 배열의 마지막 요소가 제거됨

- 반환값은 제거된 요소