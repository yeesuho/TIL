2025.07.09

Using function to create objects(함수를 사용하여 객체 생성)은 체를 생성하기 위해 함수를 생성자(constructor)처럼 사용하는 방법을 말하고 ES6 이전부터 자주 쓰이던 객체 생성 방식입니다

### 기본 개념
JavaScript에서는 함수를 이용해서 객체를 생성할 수 있죠<br> 이때 함수 이름을 대문자로 시작하고 new 키워드를 사용해서 객체를 만듭니다
```js
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.sayHello = function() {
    console.log("Hi! I'm " + this.name);
  };
}

const person1 = new Person("수호", 17);
const person2 = new Person("까미", 9);

person1.sayHello(); // Hi! I'm 수호
person2.sayHello(); // Hi! I'm 까미
```
우리집 강아지 이름이 까미라서 예시를 까미로 들겠습니다

### 작동 방식

```js
const person1 = new Person("수호", 17);
```
이렇게 new 키워드를 붙이면 JavaScript는 다음과 같이 동작합다:

1. 새로운 빈 객체 `{}`를 만든다.

2. `this`를 그 객체로 설정한다.

3. `Person` 함수 안에 있는 코드가 실행된다.

4. `this`에 속성이나 메서드가 붙는다.

5. 최종적으로 그 객체가 반환된다.


### 프로토타입 사용 (메모리 효율)
위 코드는 sayHello 함수가 객체마다 만들어지기 때문에 비효율적입니다<br>
이럴 땐 프로토타입을 활용해서 메서드를 공유하면 되죠
```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.sayHello = function() {
  console.log("Hi! I'm " + this.name);
};

const person1 = new Person("수호", 17);
const person2 = new Person("까미", 1);

person1.sayHello();
```
이 방식은 모든 `Person` 객체가 공통된 `sayHello` 함수를 공유해서 메모리 절약에 좋습니다

<br>

개념|설명
|:-:|:-:|
생성자 함수|객체를 만들기 위한 함수 (function 사용, 이름은 대문자로)
new 키워드|객체 생성, 내부에서 this 바인딩 및 객체 반환
프로토타입|함수나 속성을 공유할 수 있는 객체, 효율적

참고로 이 방식은 ES6의 class 문법으로도 바뀔 수 있습니다
```js
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  sayHello() {
    console.log("Hi! I'm " + this.name);
  }
}  
```
둘은 본질적으로 같은 원리로 동작하지만 class가 문법적으로 더 깔끔해 보이죠