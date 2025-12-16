2025.07.06

**Immutable Object(불변 객체)** 란 한 번 만들어지면 그 내용을 바꿀 수 없는 객체를 의미합니다<br>
즉 프로퍼티의 값이 수정, 추가, 삭제될 수 없는 객체이죠


### 1. 왜 Immutable Object를 사용할까
- 상태 변화를 막고 예측 가능한 코드를 작성할 수 있음

- 참조를 통해 변경되는 문제를 방지

- 리액트(React) 같은 프레임워크에서도 불변성 유지가 성능 최적화와 상태 관리에 중요

### 2. 자바스크립트에서 불변 객체 만드는 방법
### `Object.freeze()`
객체를 동결(freeze) 시켜서 수정, 추가, 삭제 모두 불가능하게 만듦
```js
const person = {
  name: "Suho",
  age: 17
};

Object.freeze(person);

person.age = 20;         // 무시됨
person.job = "student";  // 무시됨
delete person.name;      // 무시됨

console.log(person); // { name: "Suho", age: 17 }
```
>단점: 얕은(freeze) 동결이기 때문에 중첩된 객체는 변경 가능함
<br>

```js
const user = {
  name: "Suho",
  address: {
    city: "Busan"
  }
};

Object.freeze(user);

user.address.city = "Seoul"; // 변경됨 (깊은 freeze가 아님)
console.log(user.address.city); // Seoul
```

### 깊은 불변 객체 만들기 (Deep Freeze)
```js
function deepFreeze(obj) {
  Object.freeze(obj);
  Object.getOwnPropertyNames(obj).forEach(function (key) {
    if (
      typeof obj[key] === "object" &&
      obj[key] !== null &&
      !Object.isFrozen(obj[key])
    ) {
      deepFreeze(obj[key]);
    }
  });
  return obj;
}
```

## `const` vs Immutable
const는 변수를 재할당할 수 없게 하지만 객체의 속성은 바뀔 수 있고 완전한 불변성을 보장하진 않음
```js
const obj = { x: 1 };
obj.x = 2; // 가능
```
