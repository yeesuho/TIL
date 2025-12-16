2025.06.30

try...catch 문은 **에러(예외)** 가 발생할 수 있는 코드를 안전하게 실행할 수 있도록 도와주는 문법입니다

### 기본 구조
```js
try {
  // 에러가 발생할 수 있는 코드
} catch (e) {
  // 에러가 발생했을 때 실행되는 코드
}
```
### 설명
- try 블록 안에는 에러가 발생할 수 있는 코드를 넣고

- catch 블록은 에러가 발생했을 때 실행되며 에러 정보는 catch(e)의 error 변수에 담깁니다

### 예 1: 정상 동작
```js
try {
  console.log("안녕하세요");
} catch (error) {
  console.log("에러 발생:", error);
}
```

출력
```js
안녕하세요
```
에러가 없으므로 catch는 실행되지 않음


### 예 2: 에러 발생
```js
try {
  nonExistentFunction();  // 존재하지 않는 함수
} catch (e) {
  console.log("에러 발생:", e.message);
}
```
출력
```csharp
에러 발생: nonExistentFunction is not defined
```
에러가 발생했기 때문에 catch 블록이 실행됨

## 선택적으로 finally 사용
```js
try {
  // 실행 코드
} catch (error) {
  // 에러 처리
} finally {
  // 무조건 실행 (에러가 있든 없든)
}
```
finally는 예외 발생 여부와 상관없이 항상 마지막에 실행되는 블록입니다. <br>주로 정리 작업(예: 파일 닫기, 로딩 상태 해제 등)에 사용되죠


### 그럼 try catch를 왜쓸까요
1. 프로그램이 중단되지 않게 하기 위해

2. 에러 발생 시 사용자에게 친절하게 안내하기 위해

3. 디버깅 정보를 로깅하기 위해