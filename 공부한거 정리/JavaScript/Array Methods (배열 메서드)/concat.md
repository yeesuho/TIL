2025.06.24

concat()은 자바스크립트에서 배열을 합치는 데 사용되는 메서드 입니다.

### 기본 개념
```js
array1.concat(array2, array3, ..., value1, value2, ...)
```
- 여러 배열이나 값들을 하나로 합쳐서 새 배열을 만들어줌

- 원본 배열은 변경되지 않음


### 1. 배열 합치기
```js
let arr1 = [1, 2];
let arr2 = [3, 4];

let result = arr1.concat(arr2);
console.log(result); // [1, 2, 3, 4]
console.log(arr1);   // [1, 2] (원본 그대로)
```
- arr1과 arr2가 합쳐져서 새로운 배열 result가 만들어짐

### 2. 배열 + 값 합치기
```js
let arr = [1, 2];
let result = arr.concat(3, 4, 5);

console.log(result); // [1, 2, 3, 4, 5]
```
- 배열뿐 아니라 값도 직접 합칠 수 있음

### 3. 여러 개 한꺼번에 합치기
```js
let a = [1];
let b = [2, 3];
let c = [4];

let result = a.concat(b, c, 5, 6);

console.log(result); // [1, 2, 3, 4, 5, 6]
```

### 4. 중첩 배열 조심하기
```js
let arr1 = [1, 2];
let arr2 = [3, [4, 5]];

let result = arr1.concat(arr2);

console.log(result); // [1, 2, 3, [4, 5]]
```

- 중첩된 배열은 풀리지 않음
    - concat()은 1단계만 펼침 (얕은 복사)

#### 배열을 완전히 펼치고 싶으면?
```js
let result = arr1.concat(...arr2);  // ... 스프레드 연산자 사용

console.log(result);  // [1, 2, 3, 4, 5]
```

### 배열이 아닌 값을 넣어도 합쳐짐
```js
let result = [1, 2].concat('a', true, null);

console.log(result); // [1, 2, 'a', true, null]
```


### 참고: 원본은 항상 그대로
```js
let original = [100, 200];
original.concat([300]);
console.log(original); // [100, 200]
```
- 새로운 배열을 만들 뿐, original은 절대 바뀌지 않음


<br>

||설명
|:-:|:-:|
메서드명|concat()
역할|배열 또는 값을 하나로 합침
원본 배열| 변경 안 됨
반환값|새 배열
중첩 배열| 1단계만 합쳐짐 (깊게 풀지 않음)

