2025.06.24

sort()는 배열을 정렬할 때 사용하는 메서드입니다

### 기본 개념
```js
array.sort([compareFunction])
```
- 배열을 제자리에서 정렬함 => 원본 배열이 변함

- 기본 정렬은 문자열 기준으로 동작함 (즉, 유니코드 순서)

### 1. 기본 정렬 (문자열)
```js
let fruits = ['banana', 'apple', 'orange'];
fruits.sort();

console.log(fruits);  // ['apple', 'banana', 'orange']
```
- 알파벳 순서대로 정렬됨

- `compareFunction`을 안 주면 문자열 기준으로 정렬함

### 2. 숫자 정렬 (문제 발생)
```js
let nums = [10, 2, 30];
nums.sort();

console.log(nums);  // [10, 2, 30] -> 잘못 정렬됨
```
- 이유: `'10', '2', '30'`처럼 문자열로 변환되어 정렬되기 때문

그럼 어떻게 해야할까?<br>
## 숫자 정렬은 반드시 비교 함수를 써야 함
### 오름차순
```js
nums.sort((a, b) => a - b);
console.log(nums);  // [2, 10, 30]
```
### 내림차순
```js
nums.sort((a, b) => b - a);
console.log(nums);  // [30, 10, 2]
```


### compareFunction 자세히 설명

a, b를 비교했을때
1) a를 b 보다 나중에 정렬하려면 (뒤에 두려면) 0보다 큰 수를 반환
2) a를 b 보다 먼저 정렬하려면 (앞에 두려면) 0보다 작은 수를 반환
3) 원래 순서를 그대로 두려면 0을 반환

```js
array.sort((a, b) => {
  return a - b; // 오름차순
});
```
반환값|의미
|:-:|:-:|
< 0|a가 b보다 먼저
= 0|순서 유지
\> 0|b가 a보다 먼저

### 문자열 길이순 정렬
```js
let words = ['apple', 'kiwi', 'banana'];
words.sort((a, b) => a.length - b.length);

console.log(words);  // ['kiwi', 'apple', 'banana']
```


### 객체 배열 정렬
```js
let people = [
  { name: 'Suho', age: 17 },
  { name: 'Mom', age: 48 },
  { name: 'Kami', age: 8 }
];

people.sort((a, b) => a.age - b.age);

console.log(people);
// [
//   { name: 'Kami', age: 8 },
//   { name: 'Suho', age: 17 },
//   { name: 'Mom', age: 48 }
// ]
```

<br>

> 원본을 보존하려면 slice()로 복사 후 정렬해주면 됩니다