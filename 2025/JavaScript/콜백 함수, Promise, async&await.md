2025.04.13

##  콜백 함수
다른 함수에 인자로 전달되는 함수 그리고 그 함수가 어떤 작업이 끝난 뒤에 실행됨

쉽게 말해자면
### 어떤 함수에 "나중에 실행해줘" 하고 함수를 전달하는 것
```js
function 작업(callback) {
  setTimeout(() => {
    console.log("작업 끝");
    callback(); // 작업 끝나고 이 함수 실행
  }, 1000);
}


작업(() => { // 익명 화살표 함수(anonymous arrow function)
  console.log("콜백 함수 실행");
});
```

## 왜 콜백 함수를 쓸까
### 나중에 실행해야 할 코드를 미리 전달해두기 위해
예를 들어 비동기 작업이 있을 때, 작업이 끝난 후 무엇을 할지 정해주는 용도
```js
setTimeout(() => {
  console.log("3초 뒤에 실행됨");
}, 3000);
```
위에 예제 처럼
setTimeout은 3초 뒤에 함수 하나를 실행해야 하죠<br>
그래서 실행할 코드를 함수로 만들어서 넘겨주는 것 → 이게 콜백 함수

<br>

## 콜백 함수 예시
### 일반적인 콜백
```js
function greeting(name) {
  alert("Hello, " + name);
}

function processUserInput(callback) {
  const name = prompt("이름을 입력하세요.");
  callback(name);
}

processUserInput(greeting);
```
- ``processUserInput`` 안에서 greeting을 나중에 실행할 함수로 넘김

- 사용자가 입력하면 그 입력값을 greeting에 넣어 실행

###  배열 메서드와 콜백
콜백은 배열 반복 작업에서도 자주 쓰임
```js
const numbers = [1, 2, 3, 4, 5];

numbers.forEach((num) => {
  console.log(num * 2);
});
```
- ``forEach``는 배열의 각 요소마다 전달된 함수를 실행함

- 여기서는 ``(num) => { ... }`` 이게 콜백 함수이다

<br>

## 콜백 함수의 종류
### 1. 이름이 있는 함수 전달
```js
function sayHello() {
  console.log("Hello!");
}
setTimeout(sayHello, 1000);
```

### 2. 익명 함수(화살표 함수) 전달
```js
setTimeout(() => {
  console.log("Hello!");
}, 1000);
```

## 콜백 주의 사항
콜백을 너무 많이 쓰면 코드가 지옥처럼 복잡해짐
```js
login(user, () => {
  getUserData(user, (data) => {
    getPosts(data, (posts) => {
      getComments(posts, (comments) => {
        // ...
      });
    });
  });
});
```
- 이런식으로 중첩이 계속되면 가독성도 떨어지고 유지보수도 힘들어짐

- 그래서 → Promise나 async/await를 사용해서 해결하죠

