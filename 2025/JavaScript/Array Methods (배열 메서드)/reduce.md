2025.06.26

## `reduce()`는?
배열을 하나하나 줄여서 => 하나의 값을 만든다<br>
예: 합계, 평균, 객체 만들기 등 다양하게 사용 가능

###  기본 문법
```js
array.reduce((accumulator, currentValue, index, array) => {
  return 누적값;
}, 초기값);
```
매개변수|설명
|:-:|:-:|
accumulator|누적 값 (계속 쌓임)
currentValue|현재 요소
index|현재 인덱스 (옵션)
array|원본 배열 (옵션)
초기값|accumulator의 첫 시작 값

### 예시1 숫자 합 구하기
```js
let nums = [1, 2, 3, 4];

let sum = nums.reduce((acc, cur) => acc + cur, 0);
console.log(sum);  // 10
```
순서|acc|cur|결과
|:-:|:-:|:-:|:-:|
1|0|1|1
2|1|2|3
3|3|3|6
4|6|4|10

### 예시2 배열 안의 객체 -> 합계 구하기
```js
let people = [
  { name: 'Suho', age: 17 },
  { name: 'Minji', age: 20 },
  { name: 'Jisoo', age: 15 }
];

let totalAge = people.reduce((acc, person) => acc + person.age, 0);
console.log(totalAge); // 52
```

### 예시3 배열을 객체로 바꾸기
```js
let keys = ['a', 'b', 'c'];
let values = [1, 2, 3];

let result = keys.reduce((acc, key, idx) => {
  acc[key] = values[idx];
  return acc;
}, {});

console.log(result); // { a: 1, b: 2, c: 3 }
```

### 예시4 최댓값 구하기
```js
let nums = [4, 10, 2, 8];

let max = nums.reduce((acc, cur) => {
  return cur > acc ? cur : acc;
});

console.log(max);  // 10
```

## 기억할 점
- `reduce()`는 배열을 돌면서 누적한다
- 무조건 숫자만 다루는 건 아님 -> 객체, 문자열, 배열도 가능