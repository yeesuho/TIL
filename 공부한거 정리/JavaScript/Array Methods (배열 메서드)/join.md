2025.06.24

join()은 배열을 **하나의 문자열(String)** 로 합쳐주는 메서드

원래 배열은 그대로 있고 새 문자열을 만들어서 반환해줍니다

### 기본 문법
```js
array.join(separator)
```
매개변수 separator|설명
|:-:|:-:|
(선택) 문자열|요소 사이에 넣을 구분자. 생략하면 기본값은 `','`(쉼표)


### 기본 사용
```js
let fruits = ['apple', 'banana', 'orange'];
let result = fruits.join();

console.log(result); // 'apple,banana,orange'
```
- 쉼표 `,`가 자동으로 들어감 (separator를 생략했으니까)

### 다른 구분자 사용
```js
let fruits = ['apple', 'banana', 'orange'];
let result = fruits.join(' / ');

console.log(result); // 'apple / banana / orange'
```
- `' / '`를 구분자로 넣으면 그걸로 이어줌

### 빈 문자열로 이어붙이기
```js
let chars = ['H', 'e', 'l', 'l', 'o'];
let word = chars.join('');

console.log(word); // 'Hello'
```
- 구분자 없이 붙이면 문자 합치기에 좋음


### 숫자 배열도 가능
```js
let numbers = [1, 2, 3, 4, 5];
let str = numbers.join('-');

console.log(str); // '1-2-3-4-5'
```
- 숫자 배열도 문자열로 변환됨

### 활용 예시: CSV 만들기
```js
let row = ['이수호', 17, '남자'];
let csv = row.join(',');

console.log(csv); // '이수호,17,남자'
```
- 서버나 엑셀에 쓸 CSV 문자열을 만들 때 자주 씀

## 주의할 점
- null, undefined 요소는 빈 문자열로 처리됩니다
```js
let arr = ['a', undefined, 'c'];
console.log(arr.join('-')); // 'a--c'
```


## 특징 정리

특징|설명
|:-|:-|
반환값|문자열 (String)
원본 배열|변하지 않음 (비파괴적)
기본 구분자|쉼표 `,`
모든 요소는 문자열로 변환됨|숫자나 boolean도 문자열로 이어짐
