2025.06.26

map()은 배열의 각 요소를 변형해서, 새로운 배열을 만드는 함수입니다<br> 원래의 배열엔 영향을 주지 않죠
많은 상황에서 for문 대신 깔끔하게 사용됩니다<br>
그리고 자바의 map 함수랑은 아예 다른거더라고용

### 기본 문법
```js
배열.map(요소 => 바꾼값)
```
```js
array.map((element, index, array) => {
  // return 새로운 값
})
```

파라미터|설명
|:-:|:-:|
element|배열의 현재 요소
index|현재 요소의 인덱스 (생략 가능)
array|원본 배열 전체 (생략 가능)

## 핵심 특징
- 원본 배열은 변경되지 않음

- 항상 새로운 배열을 반환

- 배열의 길이는 그대로 내용만 바꿔서 새로 만듦

### 예시1 숫자 두 배로 만들기
```js
let nums = [1, 2, 3];
let doubled = nums.map(num => num * 2);

console.log(doubled); // [2, 4, 6]
console.log(nums);    // [1, 2, 3] (원본 그대로)
```

### 예시2 문자열 앞에 "Hello" 붙이기
```js
let names = ['Suho', 'Minji'];
let greetings = names.map(name => 'Hello, ' + name);

console.log(greetings); // ['Hello, Suho', 'Hello, Minji']
```

### 예시3 인덱스를 같이 쓰기
```js
let items = ['a', 'b', 'c'];
let labeled = items.map((item, index) => `${index + 1}. ${item}`);

console.log(labeled); // ['1. a', '2. b', '3. c']
```

### 예시4 객체 배열을 변형
```js
let users = [
  { name: 'Suho', age: 17 },
  { name: '까미', age: 18 }
];

let names = users.map(user => user.name);

console.log(names); // ['Suho', '까미']
```

### 예시5 조건문과 같이 쓰기
```js
let nums = [1, 2, 3, 4, 5];
let evenOrOdd = nums.map(n => n % 2 === 0 ? 'even' : 'odd');

console.log(evenOrOdd); // ['odd', 'even', 'odd', 'even', 'odd']
```

## 주의할 점
- map()은 항상 반환값을 써야 함
- 아무것도 return 하지 않으면 undefined로 채워짐
```js
let wrong = [1, 2, 3].map(n => {
  n * 2; //return을 써줘야함
});
console.log(wrong); // [undefined, undefined, undefined]
```
이럴 땐 return 꼭 쓰기