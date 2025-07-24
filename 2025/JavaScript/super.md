2025.07.24

# super란

>부모 클래스의 생성자 또는 메서드를 호출할 때 사용하는 키워드

### 생성자에서 `super`

```js
class Animal {
  constructor(name) {
    this.name = name;
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name); // 부모의 constructor 호출
    this.breed = breed;
  }
}

const myDog = new Dog("까미엄마", "까미"); //우리집 강아지가 까미임
console.log(myDog.name);  // 까미엄마
console.log(myDog.breed); // 까미
```
- 자식 클래스에서 constructor를 만들면 반드시 super()를 먼저 호출해야 함


### 메서드에서 `super`
```js
class Animal {
  speak() {
    console.log("동물이 소리를 냅니다");
  }
}

class Dog extends Animal {
  speak() {
    super.speak(); // 부모 메서드 호출
    console.log("강아지가 멍멍 짖습니다");
  }
}

const dog = new Dog();
dog.speak();
// 동물이 소리를 냅니다
// 강아지가 멍멍 짖습니다
```