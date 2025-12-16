2025.06.23

slice()는 배열의 일부를 잘라내어 복사할 때 사용하는 메서드입니다

### 기본 문법
```js
array.slice(start, end)
```
매개변수|설명
|:-:|:-:|
start|(선택) 시작 인덱스 (포함)
end|(선택) 끝 인덱스 (불포함)

- start부터 시작해서 end 바로 전까지 요소를 복사함

- end를 생략하면 끝까지 복사

- 원본 배열은 변하지 않음


### 기본 사용법

```js
let arr = ['a', 'b', 'c', 'd', 'e'];
let part = arr.slice(1, 4);

console.log(part); // ['b', 'c', 'd']
console.log(arr);  // ['a', 'b', 'c', 'd', 'e'] <= 원본은 그대로
```
- 1번 인덱스부터 4번 인덱스 직전까지

- 즉, 'b', 'c', 'd' 복사됨

### 끝까지 복사
```js
let arr = [1, 2, 3, 4, 5];
let part = arr.slice(2);  // 2번부터 끝까지

console.log(part); // [3, 4, 5]
```


### 음수 인덱스
```js
let arr = ['a', 'b', 'c', 'd'];
let part = arr.slice(-3, -1);

console.log(part); // ['b', 'c']
```
-3은 끝에서 3번째 ('b')

-1은 끝에서 1번째 ('d') → 불포함이므로 'c'까지만 포함


### 배열 복사
```js
let arr = ['x', 'y', 'z'];
let copy = arr.slice();

console.log(copy); // ['x', 'y', 'z']
```
- 인자 없이 `slice()`를 쓰면 배열 전체를 복사함