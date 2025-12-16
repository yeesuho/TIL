2025.07.01

loops(반복문)에 뭐가 있고 어떤식으로 사용하는지 봅시다

## `for` 반복문
### 기본 구조
```js
for (초기값; 조건식; 증감식) {
  // 반복 실행할 코드
}
```
### 사용 예시
```js
for (let i = 0; i < 5; i++) {
  console.log(i); // 0, 1, 2, 3, 4
}
```

<br>

## `while` 반복문
```js
while (조건식) {
  // 조건식이 참일 동안 실행
}
```
### 사용 예시
```js
let i = 0;
while (i < 5) {
  console.log(i);
  i++;
}
```

<br>

## `do...while` 반복문
### 기본 구조
```js
do {
  // 최소 1번은 실행됨
} while (조건식);
```
### 사용 예시
```js
let i = 0;
do {
  console.log(i);
  i++;
} while (i < 5);
```

- `while`이 거짓이어도 `do` 부분은 무조건 실행된다고 보면 됩니다

<br>

## `for...of` 반복문 (배열 등 반복 가능 객체용)
### 기본 구조
```js
for (const 변수 of 반복가능한객체) {
  // 요소 하나씩 꺼내서 사용
}
```

### 사용 예시
```js
const fruits = ["apple", "banana", "cherry"];
for (const fruit of fruits) {
  console.log(fruit); // apple, banana, cherry
}
```
- 배열, 문자열 등 순서가 있는 데이터에서 하나씩 꺼낼 때 사용합니다

<br>

## `for...in` 반복문 (객체용)
### 기본 구조
```js
for (const key in 객체) {
  // key는 속성 이름
}

```

### 사용 예시
```js
const person = { name: "Suho", age: 17 };
for (const key in person) {
  console.log(key, person[key]);
}
// name Suho
// age 17
```
- 객체의 속성(key)들을 하나씩 순회할 때 사용합니다

<br>

## `break`와 `continue`

### `break`: 반복문을 완전히 멈춘다
```js
for (let i = 0; i < 10; i++) {
  if (i === 5) break;
  console.log(i); // 0 ~ 4
}
```

### `continue`: 이번 반복만 건너뛰고 다음 반복으로
```js
for (let i = 0; i < 10; i++) {
  if (i % 2 === 0) continue;
  console.log(i); // 홀수만 출력됨 (1, 3, 5, 7, 9)
}
```

# 정리

반복문종류|특징|주 용도
|:-:|:-:|:-:|
`for`|반복 횟수가 명확할 때 사용|숫자 카운트 반복
`while`|조건만 만족하면 계속 반복|조건 기반 반복
`do...while`|최소 한 번 실행 보장|최초 실행 보장 후 반복 조건 확인
`for...of`|배열/문자열 등|iterable을 순회	배열 등 반복
`for...in`|객체의 key 순회|객체 속성 확인
`break` / `continue`|흐름 제어 도구|반복 제어