2025.06.29

## Copy by Value (값 복사)
```js
let a = 10;
let b = a;

b = 20;

console.log(a); // 10
console.log(b); // 20
```
- a의 값 10이 b에 복사됨

- 이후 b를 바꿔도 a에는 영향 없음

- 완전히 별개의 값

### 어떤 타입이 값 복사가 될까
- `number`

- `string`

- `boolean`

- `null`

- `undefined`

- `symbol`

- `bigint`

## Copy by Reference (참조 복사)
**객체 타입(Object Type)** 인 경우 변수에 값을 복사하면 **주소(reference)** 가 복사됨

즉 같은 객체를 가리키는 포인터를 공유함
```js
let obj1 = { name: "Suho" };
let obj2 = obj1;

obj2.name = "Timi";

console.log(obj1.name); // "Timi"
console.log(obj2.name); // "Timi"
```
- obj2 = obj1은 객체의 **주소(참조)** 를 복사한 것

- obj2를 바꾸면 obj1도 같이 바뀜

- 같은 객체를 공유함
  
### 어떤 타입이 참조 복사가 될까
- object (배열 포함)

- function

- array

- Map, Set, Date, 등등 객체 계열


왜 객체 타입은 참조 복사(reference copy)가 될까요?
그건 JavaScript의 메모리 구조와 관련이 있습니다 차근차근 알아보죠

# 메모리 구조 이해
JavaScript는 값을 저장할 때 두 가지 주요 공간을 사용함
## 스택(Stack)
- 빠르고 작음

- 기본형 데이터(number, string, boolean, 등)를 저장

- 값 자체를 저장함
## 힙(Heap)
- 크고 자유로움

- 객체 데이터(object, array, function, 등)를 저장

- **주소(reference)** 만 스택에 저장하고, 실제 데이터는 힙에 저장

### 기본형은 "값 자체"를 복사
```js
let a = 10;
let b = a;
```
- a는 스택에 10이라는 값을 가짐

- b = a는 단순히 10이라는 값을 복사해서 또 다른 공간에 저장

- 서로 전혀 관련 없음

### 객체는 "주소(reference)"를 복사
```js
let obj1 = { name: "Suho" };
let obj2 = obj1;
```
- 메모리 구조로 보면:
obj1은 스택에 있고, 실제 { name: "Suho" }는 힙에 저장됨

- obj1에는 힙 주소(ex: 0x1234)만 들어 있음

- obj2 = obj1은 그 주소값(0x1234) 를 복사함

```js
obj2.name = "Lee Suho";  // 힙의 같은 주소를 보고 있으니 obj1도 같이 바뀜
```

#### 그럼 여기서 궁금증이 생기죠 왜 이렇게 설계했을까?
### 이유 1: 효율성
- 객체는 크기가 크거나 구조가 복잡할 수 있음

- 매번 전체 객체를 복사하면 성능 낭비가 큼

- 그래서 그냥 "주소만 복사"해서 처리함 (더 빠르고 메모리 효율적이죠)

### 이유 2: 참조를 통한 공유
- 객체는 여러 곳에서 같이 사용될 수 있음

- 주소만 공유하면 데이터 일관성을 유지하기 좋음


>결론적으로 객체 타입이 참조 복사가 되는 이유는
성능, 메모리 효율, 데이터 공유를 위해
객체를 스택에 직접 저장하지 않고,
힙에 저장한 뒤 주소만 스택에 저장하기 때문인거죠