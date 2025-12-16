2025.07.20

## 비동기(Asynchronous)란?
코드가 순차적으로 실행되지 않고<br> 시간이 걸리는 작업은 "기다리지 않고" 다음 코드를 먼저 실행하는 것

### 예
```js
console.log("A");

setTimeout(() => {
  console.log("B");
}, 1000);

console.log("C");
```
#### 출력
```js
A  
C  
B  (1초 후)
```
-> 시간이 오래 걸리는 `setTimeout()`은 비동기적으로 처리됨
-> 먼저 `A`, `C` 실행 -> `B`는 1초 뒤에 실행


## `Promise` 기반 비동기 처리
```js
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve("데이터 도착"), 1000);
  });
}

fetchData().then(result => {
  console.log(result);
});
```
-  `fetchData()`는 `Promise`를 반환하고, `.then()`으로 결과를 처리함
  

## `async` / `await`란?
Promise를 더 직관적인 방식으로 다루게 해주는 문법

`async`: 함수를 비동기 함수로 선언

`await`: Promise가 끝날 때까지 기다림

### 예시
```js
async function getData() {
  console.log("요청 시작");

  const result = await fetchData(); // 기다림

  console.log("응답:", result);
}

getData();
```

#### 출력
```js
요청 시작  
(1초 뒤)  
응답: 데이터 도착!
```

키워드|설명
|:-:|:-:|
async|해당 함수가 항상 Promise를 반환하도록 함
await|Promise가 해결(resolve)될 때까지 기다림
await는 어디서 사용 가능?|반드시 async 함수 안에서만
에러 처리|try/catch로 간단하게 가능


### 에러 처리도 간단히
```js
async function getData() {
  try {
    const result = await fetchData();
    console.log("응답:", result);
  } catch (error) {
    console.log("에러 발생:", error);
  }
}
```