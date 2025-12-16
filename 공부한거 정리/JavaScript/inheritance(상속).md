2025.07.23

## 상속 (Inheritance)
>**부모 클래스(기존 클래스)** 의 속성과 메서드를 **자식 클래스(새 클래스)** 가 물려받는 것

```js
class Animal {
  speak() {
    console.log("동물이 소리를 냅니다");
  }
}

class Dog extends Animal {
  bark() {
    console.log("멍멍");
  }
}

const myDog = new Dog();
myDog.speak(); // 동물이 소리를 냅니다 (Animal에서 상속받음)
myDog.bark();  // 멍멍 (Dog 고유 메서드)
```
- Dog는 Animal을 상속받음

- extends 키워드로 상속 선언


