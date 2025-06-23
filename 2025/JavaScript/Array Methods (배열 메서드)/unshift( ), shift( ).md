2025.06.23

unshift()와 shift()는 push()/pop()의 반대<br> 방향
배열의 **앞쪽(맨 앞 요소)** 을 다루는 메서드들

### ``unshift()``: 배열의 앞에 요소 추가
```js
let fruits = ['banana', 'orange'];
fruits.unshift('apple');

console.log(fruits);  // ['apple', 'banana', 'orange']
```
- 'apple'이 배열 맨 앞에 추가됨

- 반환값은 추가 후 배열의 길이

### ``shift()``: 배열의 앞 요소 제거
```js
let fruits = ['apple', 'banana', 'orange'];
let first = fruits.shift();

console.log(fruits);  // ['banana', 'orange']
console.log(first);   // 'apple'
```
- 배열 맨 앞의 요소가 제거됨

- 반환값은 제거된 요소


## 단점
### ``shift()`` / ``unshift()``는 성능이 느림
- 배열의 맨 앞 요소를 추가하거나 제거하면
- 나머지 요소들의 인덱스를 전부 한 칸씩 이동시켜야 함
```js
let arr = ['a', 'b', 'c', 'd'];
arr.shift();  // 'a' 제거

// 내부적으로 이런 일이 일어남:
// 'b' → 0번 인덱스로 이동
// 'c' → 1번 인덱스로 이동
// 'd' → 2번 인덱스로 이동
```
이건 요소가 많을수록 오래 걸리게 됨
<br>
즉 시간복잡도가 O(n) (n은 배열 길이)

### 반면, ``push()`` / ``pop()``은 빠름
- 배열 끝쪽만 건드리므로 인덱스 재조정이 필요 없음
- 시간복잡도 O(1) 이라 효율적임