2025.07.05

Property Attribute는 객체의 **속성(Property)** 이 가지는 **특성(속성의 속성)** 을 의미합니다<br>
쉽게 말하면 어떤 객체의 프로퍼티가 읽기 전용인지, 삭제 가능한지, 반복문에 노출되는지 등을 결정하는 메타정보입니다

## 자바스크립트의 프로퍼티 어트리뷰트 종류
### 데이터 프로퍼티(Data Property)
일반적인 값을 갖는 프로퍼티<br>
아래 4가지 어트리뷰트를 가짐:
어트리뷰트|이름	설명
|:-:|:-:|
value|프로퍼티에 저장된 값
writable|값을 수정할 수 있는지 여부 (`true`/`false`)
enumerable|`for...in`이나 `Object.keys()`로 열거 가능한지 여부
configurable|삭제 가능 여부, 어트리뷰트 수정 가능 여부
```js
const user = {};
Object.defineProperty(user, "name", {
  value: "Suho",
  writable: true,       // 값 변경 가능
  enumerable: true,     // 반복문에서 보임
  configurable: true    // 삭제 가능, 속성 재정의 가능
});

console.log(user.name); // Suho
```

### 접근자 프로퍼티(Accessor Property)
값을 갖기보단 getter/setter 함수로 정의된 프로퍼티
어트리뷰트 이름|설명
|:-:|:-:|
get|값을 읽을 때 호출되는 함수
set|값을 설정할 때 호출되는 함수
enumerable|반복문에 노출 여부
configurable|삭제 및 속성 변경 가능 여부
```js
const person = {
  firstName: "Su",
  lastName: "Ho",

  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  },

  set fullName(name) {
    [this.firstName, this.lastName] = name.split(" ");
  }
};

console.log(person.fullName); // Su Ho
person.fullName = "Lee Suho";
console.log(person.firstName); // Lee
```

## 속성 확인 방법
Object.getOwnPropertyDescriptor()를 사용하면 어트리뷰트를 볼 수 있습니다
```js
const obj = { x: 10 };

const desc = Object.getOwnPropertyDescriptor(obj, 'x');
console.log(desc);
// 출력:
// {
//   value: 10,
//   writable: true,
//   enumerable: true,
//   configurable: true
// }
```

## 기본적으로 생성되는 프로퍼티의 속성
```js
const obj = { x: 1 };
```
위처럼 생성된 프로퍼티는 기본적으로:

- `writable: true`

- `enumerable: true`

- `configurable: true`