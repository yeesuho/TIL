2025.06.24

## ``spread operator (...)``
`...` 스프레드 연산자 


### 기본 개념
```js
let arr = [1, 2, 3];
console.log(...arr); // 1 2 3
```
- ...arr은 배열을 한 칸 한 칸씩 펼쳐서 보여줌

- [1, 2, 3]이 아니라 -> 1, 2, 3 이렇게 배열을 펼쳐서


### 배열 합치기 (concat 대체 가능함)
```js
let arr1 = [1, 2];
let arr2 = [3, 4];

let result = [...arr1, ...arr2];
console.log(result);  // [1, 2, 3, 4]
```
- concat()처럼 합치지만 더 직관적이고 간단함

- 그냥 펼쳐서 붙이는 느낌


### 배열 복사
```js
let original = [10, 20, 30];
let copy = [...original];

copy[0] = 99;

console.log(original); // [10, 20, 30] <= 원본 안 바뀜
console.log(copy);     // [99, 20, 30]
```
- copy = original 하면 연결돼버리지만,

- copy = [...original] 하면 완전히 새 배열이 만들어집니다

### 객체 복사 및 병합
```js
let user = { name: 'Suho', age: 17 };
let copy = { ...user, age: 18 };  // age만 덮어쓰기

console.log(copy);  // { name: 'Suho', age: 18 }
```
- 객체도 펼쳐서 복사 가능

- 뒤에 있는 속성이 앞을 덮어씀 (우선순위)

### 함수 인자 전달
```js
function add(x, y, z) {
  return x + y + z;
}

let nums = [1, 2, 3];
console.log(add(...nums));  // 6
```
- 배열을 각각의 인자처럼 전달할 수 있음
- `add(1, 2, 3)`와 같은 효과