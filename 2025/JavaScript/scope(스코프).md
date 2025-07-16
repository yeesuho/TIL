2025.07.16

자바스크립트의 스코프(Scope)는 변수가 어디서 선언되고 접근 가능한지를 결정하는 아주 중요한 개념입니다

## 스코프란?
스코프(Scope)란 변수, 함수, 객체 등이 접근 가능한 유효 범위를 말해. 자바스크립트는 **Lexical Scope (정적 스코프)** 를 따르기 때문에, 코드를 작성한 위치를 기준으로 스코프가 결정됩니다

### 스코프의 종류
글로벌 스코프 (Global Scope)
- 함수 밖에서 선언된 변수는 어디서든 접근 가능
- 전역 스코프라고도 합니다
```js
var a = 10;
function foo() {
  console.log(a); // 10
}
foo();
```

### 함수 스코프 (Function Scope)
- `var`, `let`, `const` 모두 함수 안에서 선언된 변수는 함수 안에서만 접근 가능

```js
function test() {
  var x = 5;
  console.log(x); // 5
}
console.log(x); // 오류 (함수 밖에서는 접근 불가)
```

### 블록 스코프 (Block Scope)
- { } 중괄호 안의 범위
- let, const는 블록 레벨 스코프를 가지며, var는 가지지 않음
```js
if (true) {
  var a = 1;
  let b = 2;
  const c = 3;
}
console.log(a); // 1 (var는 블록 스코프 없음)
console.log(b); // 오류
console.log(c); // 오류
```