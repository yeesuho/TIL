2025.06.28

객체는 하나 이상의 **속성(프로퍼티)** 을 가진 자료형이고, 이 속성은 **키(key)와 값(value)** 의 쌍으로 이루어져 있습니다

아래에서 차근 차근 알아보죠

## 객체(Object)란
객체는 관련된 데이터를 하나로 묶어서 표현하는 자료형입니다.
```js
const person = {
  name: "Suho",
  age: 17,
  isStudent: true
};
```
- name, age, isStudent → 각각 key (속성 이름)
- "Suho", 17, true → 각각 value (속성 값)

### 객체 생성 방법
#### 리터럴 방식 (가장 흔함)
```js
const dog = {
  name: "Max",
  breed: "Golden Retriever"
};
```

#### 생성자 방식
```js
const dog = new Object();
dog.name = "Max";
dog.breed = "Golden Retriever";
```

### 속성 접근 (dot vs bracket)
```js
const user = {
  id: "suho123",
  "user name": "이수호"
};

console.log(user.id); // dot notation
console.log(user["user name"]); // bracket notation (공백이 있을 땐 이 방법만 가능)
```

### 속성 추가, 수정, 삭제
```js
const user = {
  name: "Suho"
};

// 추가
user.age = 17;

// 수정
user.name = "Lee Suho";

// 삭제
delete user.age;
```

### 객체 안에 함수: 메서드
```js
const calculator = {
  add: function (a, b) {
    return a + b;
  }
};

console.log(calculator.add(2, 3)); // 5
```
이렇게 객체 안에 정의된 함수를 **메서드(method)** 라고 불릅니다

### this 키워드
객체 내부에서 this는 **자기 자신(그 객체)** 을 가리킵니다
```js
const person = {
  name: "Suho",
  greet: function () {
    console.log("Hello, I’m " + this.name);
  }
};

person.greet(); // Hello, I’m Suho
```

### 객체 반복
```js
const book = {
  title: "AI 시대",
  author: "Suho",
  year: 2025
};

for (let key in book) {
  console.log(key + ": " + book[key]);
}
```

### 객체 안에 객체 (중첩 객체)
```js
const user = {
  name: "Suho",
  address: {
    city: "Seoul",
    zip: "12345"
  }
};

console.log(user.address.city); // Seoul
```

## 객체 관련 함수들
`Object.keys(obj)` → 키 배열 반환

`Object.values(obj)` → 값 배열 반환

`Object.entries(obj)` → [key, value] 배열 반환

`Object.assign(target, source)` → 객체 복사

`JSON.stringify(obj)` → 문자열로 변환

`JSON.parse(str)` → 문자열을 객체로 변환

```js
const user = { name: "Suho", age: 17 };

console.log(Object.keys(user)); // ["name", "age"]
console.log(Object.values(user)); // ["Suho", 17]
console.log(Object.entries(user)); // [["name", "Suho"], ["age", 17]]
```

### 얕은 복사 vs 깊은 복사
```js
const original = { name: "Suho" };
const copy = original; // 얕은 복사 (같은 참조)

copy.name = "Lee";
console.log(original.name); // "Lee"
```
>같은 메모리 주소를 가리키기 때문에 원본도 바뀜

>깊은 복사는 `structuredClone(original)` 또는 `JSON.parse(JSON.stringify(original))` 사용