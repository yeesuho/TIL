2025.07.18

## this란?
자바스크립트에서 this는 "현재 실행 중인 컨텍스트(문맥)"에서의 객체를 가리킵니다 <br>
간단히 말해, **"누가 호출했느냐"** 에 따라 this의 값이 달라지죠

### 1. 전역 컨텍스트에서의 this
```js
console.log(this);  // 브라우저: window / Node.js: global
```
- 브라우저에서는 `this === window`

- Node.js에서는 `this === global` (단, 모듈 안에서는 undefined일 수도 있음)

### 2. 객체의 메서드에서의 this
```js
const user = {
  name: "Suho",
  greet: function() {
    console.log(this.name);
  }
};

user.greet(); // Suho
```
- this는 메서드를 호출한 객체 (user) 를 가리킴

### 3. 함수에서의 this (일반 함수 호출)
```js
function sayHi() {
  console.log(this);
}

sayHi(); // 브라우저: window / 엄격 모드(strict): undefined
```
- 그냥 호출된 함수의 this는 전역 객체

- 'use strict' 모드에서는 undefined

### 4. 생성자 함수에서의 this
```js
function Person(name) {
  this.name = name;
}

const p1 = new Person("Alice");
console.log(p1.name); // Alice
```
- `new`와 함께 호출하면 `this`는 새로 만들어지는 객체를 가리킴

### 5. this를 잃어버리는 예 (중요)
```js
const user = {
  name: "Suho",
  greet: function() {
    console.log(this.name);
  }
};

const fn = user.greet;
fn(); // undefined (전역에서 호출됨)
```
- `fn()`은 `user`와의 연결이 끊겨서 `this`는 전역 객체

- 해결하려면 bind, call, apply 또는 화살표 함수 사용

### 6. 화살표 함수의 this
```js
const user = {
  name: "Suho",
  greet: () => {
    console.log(this.name);
  }
};

user.greet(); // undefined
```
- ⚠️ 화살표 함수는 this를 갖지 않음

- 대신 자기 스코프의 this를 상속함

<br>

```js
function Timer() {
  this.sec = 0;

  setInterval(() => {
    this.sec++;
    console.log(this.sec);
  }, 1000);
}
```
- 위의 예에서 `this.sec++`은 `Timer` 객체의 `this`를 그대로 사용함


### 7. call, apply, bind로 this를 바꾸기
```js
function sayName() {
  console.log(this.name);
}

const user = { name: "Suho" };
const admin = { name: "Admin" };

sayName.call(user);   // Suho
sayName.apply(admin); // Admin

const boundFn = sayName.bind(user);
boundFn(); // Suho
```
- `call(thisArg, ...)`: this 지정하고 실행

- `apply(thisArg, [args])`: call이랑 같지만 인자 배열

- `bind(thisArg)`: this를 바인딩한 새 함수 반환

