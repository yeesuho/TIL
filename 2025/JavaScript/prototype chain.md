2025.07.15

prototype chain은 객체 지향 프로그래밍의 핵심 개념 중 하나입니다<br> 객체 간에 **상속(inheritance)** 을 구현하는 방법이죠<br> 쉽게 말해, 어떤 객체가 가지고 있지 않은 속성이나 메서드를 "위로 거슬러 올라가며(prototype chain을 따라)" 찾는 구조입니다

### 핵심 개념
#### 1. 모든 객체는 **prototype(프로토타입)** 을 가진다
- 자바스크립트의 객체는 생성될 때 [[Prototype]] 이라는 숨겨진 프로퍼티를 가짐

- 이 프로퍼티는 또 다른 객체를 가리키며, 그 객체가 부모 객체 역할을 함

- 자바스크립트에서는 __proto__ 또는 Object.getPrototypeOf(obj)로 접근 가능
```js
const person = {
  greet: function () {
    console.log("Hello!");
  }
};

const student = {
  study: function () {
    console.log("Studying...");
  }
};

// student의 prototype을 person으로 설정
student.__proto__ = person;

student.greet(); // Hello!  (person에서 찾아옴)
student.study(); // Studying...
```
#### 2. 프로토타입 체인의 동작 방식
- 어떤 속성이나 메서드를 객체에서 찾을 때:

    1.객체 자신에게 있는지 확인

    2. 없으면 __proto__로 올라가서 부모 객체에서 찾음

    3. 계속 위로 올라감

    4. 마지막엔 Object.prototype까지 올라감

    5. 거기에도 없으면 undefined

## 예시로 보는 프로토타입 체인
```js
function Animal() {}
Animal.prototype.sayHi = function () {
  console.log("Hi from Animal");
};

function Dog() {}
Dog.prototype = Object.create(Animal.prototype); // Animal을 상속받음
Dog.prototype.constructor = Dog;

const myDog = new Dog();

myDog.sayHi(); // Hi from Animal
```
- `myDog` → `Dog.prototype` → `Animal.prototype` → `Object.prototype`
- 이게 바로 프로토타입 체인


## 왜 중요할까?
- 상속 없이도 객체 간에 기능을 공유할 수 있음

- 자바스크립트의 모든 내장 객체도 이 구조로 만들어짐

- Array, Function, Date 등도 Object에서 상속받음