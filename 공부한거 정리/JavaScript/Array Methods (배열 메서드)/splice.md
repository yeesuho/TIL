2025.06.23

### 기본 문법
```js
array.splice(start, deleteCount, item1, item2, ...)
```
|||
|:-:|:-:|
start|변경을 시작할 인덱스 (0부터 시작)
deleteCount|제거할 요소 개수
item1, 2, ...|삽입할 요소 (없으면 삭제만 됨)

### 1. 삭제만 하기
```js
let arr = ['a', 'b', 'c', 'd'];
arr.splice(1, 2); // 1번 인덱스부터 2개 삭제

console.log(arr);  // ['a', 'd']
```
- 'b', 'c'가 삭제됨

- start=1, deleteCount=2

### 2. 추가만 하기
```js
let arr = ['a', 'b', 'c'];
arr.splice(1, 0, 'x', 'y');

console.log(arr);  // ['a', 'x', 'y', 'b', 'c']
```
- deleteCount = 0 이라 삭제는 안 하고

- 1번 자리에 'x', 'y'가 삽입됨

### 3. 삭제 + 추가 = 교체
```js
let arr = ['a', 'b', 'c'];
arr.splice(1, 1, 'x');

console.log(arr);  // ['a', 'x', 'c']
```
- 'b'를 제거하고, 'x'로 교체한 셈

### 반환값
splice()는 제거된 요소들을 배열로 반환해줌
```js
let arr = ['a', 'b', 'c', 'd'];
let removed = arr.splice(1, 2);

console.log(removed);  // ['b', 'c']
```

### 음수 인덱스도 가능
```js
let arr = ['a', 'b', 'c', 'd'];
arr.splice(-2, 1, 'x');  // 끝에서 두 번째 자리를 'x'로 교체

console.log(arr);  // ['a', 'b', 'x', 'd']
```
-2는 arr.length - 2와 같음


## 주의
- 원본 배열이 직접 변경됨
  - 기존 데이터를 유지하고 싶으면 복사해두기
- splice는 매우 유연하지만 너무 자주 쓰면 코드 가독성이 떨어질 수 있음