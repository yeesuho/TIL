2025.07.21

자바스크립트의 **콜백 헬(callback hell)** 과 이를 해결하기 위한 프로미스(Promise) 개념을 이해하는 건 비동기 프로그래밍의 핵심이니 한번 복습해봅시다

### Callback(콜백)부터 이해하자
>콜백(callback)은 어떤 함수의 인자로 넘겨지는 함수입니다<br>보통 비동기 작업이 끝난 뒤 실행될 작업을 전달할 때 사용하죠

```js
function doSomething(callback) {
  setTimeout(() => {
    console.log("일 완료");
    callback();
  }, 1000);
}

doSomething(() => {
  console.log("다음 작업 실행");
});
```

### Callback Hell이란?
>콜백 안에 콜백이 중첩되면서 코드가 너무 복잡해지는 현상
```js
setTimeout(() => {
  console.log("1번 작업");
  setTimeout(() => {
    console.log("2번 작업");
    setTimeout(() => {
      console.log("3번 작업");
      // ...
    }, 1000);
  }, 1000);
}, 1000);
```
#### 문제점:
- 들여쓰기 많음

- 가독성 나쁨

- 에러 처리 어려움

- 유지보수 최악

이런 걸 "callback hell" 또는 **"pyramid of doom(파멸의 피라미드)"** 라고 불른답니다


## Promise란?
>콜백 헬을 해결하기 위해 등장한 ES6 비동기 처리 객체
### Promise의 3가지 상태
- Pending: 대기 중

- Fulfilled: 성공(resolve)

- Rejected: 실패(reject)
```js
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("성공");
  }, 1000);
});

promise.then((result) => {
  console.log(result); // 성공
}).catch((error) => {
  console.log(error);
});
```


### Promise로 콜백 헬 해결하기
```js
function task1() {
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log("1번 작업");
      resolve();
    }, 1000);
  });
}

function task2() {
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log("2번 작업");
      resolve();
    }, 1000);
  });
}

function task3() {
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log("3번 작업");
      resolve();
    }, 1000);
  });
}

// 깔끔하게 연결
task1()
  .then(() => task2())
  .then(() => task3())
  .then(() => {
    console.log("모든 작업 완료");
  });
```


### 비교 하기

||Callback Hell|Promise
|:-:|:-:|:-:|
구조|중첩 콜백 지옥|체이닝 구조 
가독성|나쁨|좋음
에러 처리|복잡|`.catch()`로 간단
유지보수|어렵다|쉽다