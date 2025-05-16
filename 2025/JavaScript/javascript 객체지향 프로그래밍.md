2025.05.16

JavaScript는 **객체지향 프로그래밍(OOP, Object-Oriented Programming)**이 가능한 언어입니다<br>
다만 자바처럼 클래스 기반보다는 원래는 프로토타입 기반 객체지향 언어였지만 지금은 지금은 둘 다 지원합니다

#### 프로토타입 기반 언어란
모든 객체는 "프로토타입"이라는 숨겨진 부모를 가지고 있고
<br>
객체가 어떤 속성이나 메서드를 찾을 때 자기 자신 → 부모(프로토타입) → 그 부모의 부모... 이런 식으로 프로토타입 체인을 따라가며 찾는 구조

### 예시)
```js
function Animal(name) {
  this.name = name;
}

Animal.prototype.speak = function () {
  console.log(`${this.name}가 소리를 냅니다.`);
};

const dog = new Animal("강아지");
dog.speak(); // 강아지가 소리를 냅니다.
```
- dog는 speak()라는 메서드를 직접 가지고 있지 않음

- 근데 Animal.prototype에 정의되어 있으니까 dog가 그걸 "물려받아" 쓸 수 있는 것

- 이것이 바로 프로토타입 상속

### 비유로 쉽게 설명하면
클래스 기반 객체지향 언어는 **설계도(클래스)** 를 먼저 만들고 그걸로 **건물(객체)** 을 짓는 방식

프로토타입 기반 객체지향 언어는 **기존 건물(객체)** 에서 새로운 건물을 **복사 + 변경**해서 만드는 방식

서론이 길었고 본론으로 들어가겠습니다
## 객체지향이란?
실생활처럼 데이터를 **객체**로 묶어서
**속성(=변수, 상태)** 과 **동작(=함수, 행동)** 을 같이 다루는 방식

예를 들어 "강아지" 객체:
```js
let dog = {
  name: "까미", // 실제 우리집 강아지 이름
  bark: function() {
    console.log("멍멍");
  }
};

dog.bark(); // 멍멍
```

### 생성자 함수 (ES5 스타일)
```js
function Animal(name) {
  this.name = name;
  this.speak = function() {
    console.log(this.name + "이(가) 소리를 냅니다.");
  };
}

let dog = new Animal("강아지");
dog.speak(); // 강아지이(가) 소리를 냅니다.
```

### 프로토타입 기반 상속
```js
function Animal(name) {
  this.name = name;
}
Animal.prototype.speak = function() {
  console.log(this.name + "이(가) 소리를 냅니다.");
};

let cat = new Animal("고양이");
cat.speak(); // 고양이이(가) 소리를 냅니다.
```
prototype을 사용하면 여러 객체가 같은 함수 메모리를 공유해서 성능이 좋아진답니다

### 클래스 문법 (ES6 이후)
```js
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name}이(가) 소리를 냅니다.`);
  }
}

const lion = new Animal("사자");
lion.speak(); // 사자이(가) 소리를 냅니다.
```

### 상속(extends)
```js
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name}이(가) 소리를 냅니다.`);
  }
}

class Dog extends Animal {
  bark() {
    console.log("멍멍!");
  }
}

const myDog = new Dog("코코");
myDog.speak(); // 코코이(가) 소리를 냅니다.
myDog.bark();  // 멍멍!
```

## 문법 정리
|문법|설명
|:-:|:-:|
``class``|클래스를 정의
``constructor()``|생성자 함수 (객체 초기화)
``extends``|상속
``super()``|부모 클래스 호출
``prototype``|생성자 기반 객체 공유 메서드

## 캡슐화, 다형성, 상속 정리

|개념|설명|예시
|:-:|:-:|:-:|
캡슐화|객체 안에 상태(변수)와 동작(함수)을 묶기|``this.name, speak()``
상속|부모의 기능을 자식이 물려받기|``class Dog extends Animal``
다형성|같은 speak()가 동물마다 다르게 동작|오버라이딩 가능

