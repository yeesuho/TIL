2025.07.19

# 클로저(Closur)란?
>"함수가 선언될 때의 외부 변수(스코프)를 기억하고, 나중에 그 변수에 접근할 수 있는 함수"

함수가 끝났는데도 바깥에 있는 변수를 기억하고 접근할 수 있는 상태를 말합니다

### 가장 기본적인 클로저
```js
function outer() {
  let count = 0;

  function inner() {
    count++;
    console.log(count);
  }

  return inner;
}

const counter = outer();  // outer는 종료됐지만
counter(); // 1
counter(); // 2
```
설명:
- `inner`는 `count`를 사용하고 있음

- `outer()`는 호출된 뒤 종료됐지만
`inner`는 `count`를 기억하고 계속 접근 가능합니다

- 이게 바로 클로저

### 클로저는 언제 쓰일까?
#### 1. 상태 유지
```js
function makeCounter() {
  let count = 0;
  return () => ++count;
}

const counter = makeCounter();
console.log(counter()); // 1
console.log(counter()); // 2
```
- 외부에서 `count`에 직접 접근 못하고,

- 오직 `counter()`를 통해서만 증가 가능 → 캡슐화

#### 2. 비동기/타이머에서 값 기억
```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000);
}
// 출력: 3 3 3 (var는 함수 스코프)

for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000);
}
// 출력: 0 1 2 (let은 블록 스코프 + 클로저)
```
- 클로저 덕분에 각 반복의 `i` 값이 보존됨


#### 3. 함수형 프로그래밍, 콜백, 이벤트 리스너 등에서 자주 사용

<br>

> 요약하자면 클로저는 함수가 외부 변수(상위 스코프)를 기억해서, 함수 실행이 끝난 후에도 사용할 수 있는 것 입니다

|||
|:-:|:-:|
스코프|변수에 접근 가능한 범위
렉시컬 스코프|함수가 선언된 위치 기준으로 스코프 결정
클로저|선언 당시의 스코프를 기억하고, 나중에도 변수에 접근 가능한 함수