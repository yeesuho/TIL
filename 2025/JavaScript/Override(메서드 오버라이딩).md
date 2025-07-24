2025.07.24

## 메서드 오버라이딩 (Override)

>자식 클래스에서 부모와 같은 이름의 메서드를 다시 정의하는 것

```js
class Animal {
  sound() {
    console.log("동물 소리");
  }
}

class Cat extends Animal {
  sound() {
    console.log("야옹");
  }
}

const cat = new Cat();
cat.sound(); // 야옹  <- override된 메서드가 실행됨
```
- 부모 메서드와 같은 이름이지만, 자식에서 재정의한 메서드가 우선 실행됨
