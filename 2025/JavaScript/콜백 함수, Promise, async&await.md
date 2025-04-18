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


<br>

2025.04.16

# Promise

Promise는 비동기 작업의 결과를 나중에 받을 수 있게 해주는 객체입니다<br>
예를 들자면 서버에서 데이터를 받아오기, 파일 읽기, 타이머 (setTimeout)<br>
이런 작업들은 시간이 걸리기 때문에, 기다리지 않고 다음 코드로 넘어가려고 비동기 방식으로 처리합니다<br>
그래서 자바스크립트에서 "나중에 결과가 오면 알려줄게"라고 약속하는게<br>
바로 Promise입니다

### 왜 Promise가 필요할까
예전에는 **콜백 함수(callback)** 로 비동기 처리를 많이 했지만 콜백 안에 또 콜백, 또 콜백이 들어가다보면..
```js
doSomething(function(result1) {
  doSomethingElse(result1, function(result2) {
    doAnotherThing(result2, function(result3) {
      // ...
    });
  });
});
```
이런식으로 콜백 지옥이 발생하게 됨 그래서 나온 게 Promise입니다

사용법 에시)
```js
// 1초 후에 "완료"라고 알려주는 Promise 만들기
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("완료");
  }, 1000);
});

// 결과를 받아서 출력
myPromise.then(result => {
  console.log("결과:", result);  // 결과: 완료
});
```

<br>

## 세가지 상태
Promise는 비동기 작업의 "진행 상태"를 나타내는 **세 가지 상태(state)** 를 가질 수 있습니다

### pending (대기 상태)
의미:
- 비동기 작업이 아직 끝나지 않음

- 결과도 없고, 에러도 없음

ex)
```js
const p = new Promise((resolve, reject) => {
  // 3초 뒤에 결과를 줄 예정
  setTimeout(() => {
    resolve("끝");
  }, 3000);
});
```
이 코드를 실행하 처음에는 p는 pending 상태입니다<br>
아무일도 안일어나죠

### fulfilled (성공 상태)
의미:
- 비동기 작업이 성공적으로 끝남

- resolve()를 호출해서 결과를 줬음

ex)
```js
const p = new Promise((resolve, reject) => {
  resolve("성공");
});

p.then(result => {
  console.log(result); // "성공"
});
```
resolve("성공")이 실행되면 상태가 fulfilled로 바뀌고<br>
.then(...) 안에 있는 코드가 실행됩니다

<br>

### rejected (실패 상태)
의미:
- 비동기 작업이 실패함

- reject()를 호출하거나 에러가 발생함

ex)
```js
const p = new Promise((resolve, reject) => {
  reject("에러 발생");
});

p.catch(error => {
  console.log(error); // "에러 발생"
});
```
reject("에러 발생")이 실행되면 상태는 rejected로 바뀌고
.catch(...) 안에 있는 코드가 실행됩니다

<br>
흐름

```css
[처음 상태]
→ pending

[resolve 호출되면]
→ fulfilled

[reject 호출되면]
→ rejected
```
그리고 한 번 fulfilled나 rejected 상태가 되면
다시는 pending으로 돌아갈 수 없습니다 (한 번 결정나면 끝)

## Promise 생성 방법
```js
const myPromise = new Promise((resolve, reject) => {
  // 여기에 비동기 작업
  const success = true;

  if (success) {
    resolve("성공");
  } else {
    reject("실패");
  }
});
```
- ``resolve()`` → 성공했을 때

- ``reject()`` → 실패했을 때


## .then() / .catch()
### then이 뭐죠
=> 성공했을 때 실행되는 코드<br>
Promise가 성공적으로 끝났을 때 (resolve가 호출됐을 때)
그 결과를 받아서 처리하는 함수입니닷
### 그럼 catch는 실패했을 때 쓰는건가
=> 맞음 Promise가 실패했을 때 (reject가 호출됐을 때)
에러나 문제를 처리하는 함수입니다

### then과 catch를 같이 쓰면?
```js
const p = new Promise((resolve, reject) => {
  const success = false;
  if (success) {
    resolve("성공");
  } else {
    reject("실패");
  }
});

p.then((result) => {
  console.log("성공:", result);
})
.catch((error) => {
  console.log("실패:", error);
});
```
성공하면 .then(...)이 실행되고

실패하면 .catch(...)가 실행

2025.04.17

# async & await

