2025.6.26

filter()는 배열에서 조건을 만족하는 요소만 골라내는 메서드입니다<br>
말 그대로 필터처럼 걸러주는 역할을 하죠

### 기본 문법
```js
배열.filter(요소 => 조건식)
```
```js
array.filter((element, index, array) => {
  return 조건;
});
```
매개변수|설명
|:-:|:-:|
element|지금 검사하는 배열의 요소
index|그 요소의 인덱스 (생략 가능)
array|원본 배열 전체 (생략 가능)

### 예시1 짝수 필터링
```js
let nums = [1, 2, 3, 4, 5, 6];
let evens = nums.filter(n => n % 2 === 0);

console.log(evens); // [2, 4, 6]
```

### 예시2 길이가 4 이상인 문자열만 추출
```js
let words = ['hi', 'hello', 'cat', 'tiger'];
let longWords = words.filter(word => word.length >= 4);

console.log(longWords); // ['hello', 'tiger']
```

### 예시3 객체 배열에서 조건에 맞는 요소만
```js
let users = [
  { name: 'Suho', age: 17 },
  { name: 'Minji', age: 20 },
  { name: 'Jisoo', age: 15 }
];

let adults = users.filter(user => user.age >= 18);

console.log(adults);
// [ { name: 'Minji', age: 20 } ]
```

<br>

## 주의할 점
- filter()는 항상 true/false를 판단하는 식을 써야 함

- return이 빠지거나 조건이 없다면 undefined로 판단되고 모두 걸러질 수도 있음
```js
let wrong = [1, 2, 3].filter(n => {
  n > 1;  // return이 없어서 안 됨
});
console.log(wrong); // []
```
`return`을 써줘야함
```js
let correct = [1, 2, 3].filter(n => {
  return n > 1;
});
```

### map()과 비교
메서드|용도|반환
|:-:|:-:|:-:|
`map()`|배열의 요소를 변형|새로운 배열 (길이 유지됨)
`filter()`|배열의 요소를 선별|새로운 배열 (길이 줄어들 수 있음)

