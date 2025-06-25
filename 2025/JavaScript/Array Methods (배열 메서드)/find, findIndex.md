2025.06.26

## `find()`: 조건에 맞는 첫 번째 요소를 "값"으로 반환
```js
array.find(요소 => 조건식)
```

예시)
```js
let numbers = [1, 3, 5, 8, 10];

let found = numbers.find(num => num > 5);
console.log(found);  // 8
```
- 조건을 만족하는 첫 요소 8을 찾아서 반환

- 여러 개가 있어도 가장 먼저 찾은 것 1개만

- 조건에 맞는 게 없으면 undefined 반환

## `findIndex()`: 조건에 맞는 첫 번째 요소의 인덱스를 반환
```js
array.findIndex(요소 => 조건식)
```

예시)
```js
let numbers = [1, 3, 5, 8, 10];

let index = numbers.findIndex(num => num > 5);
console.log(index);  // 3
```
- 8은 인덱스 3에 있으므로 3이 반환됨

- 조건에 맞는 게 없으면 -1 반환

>`filter()`는 여러 개를 **"모두"** 찾고

>`find()`는 조건을 만족하는 **"첫 번째 것"** 만 찾음