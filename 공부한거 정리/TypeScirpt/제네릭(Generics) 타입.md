2025.03.30

**제네릭 타입(Generics)** 은 타입을 나중에 지정할 수 있도록 하는 기능<br>
"어떤 타입이 들어올지 나중에 정할 수 있도록" 만드는 것 <br>
예를 들어, 특정 함수나 클래스, 인터페이스에서 타입을 유연하게 처리하고 싶을 때 제네릭을 사용

## 제네릭 함수
제네릭을 사용하면 함수의 매개변수와 반환값에 타입을 동적으로 지정 가능
```typescript
function identity<T>(value: T): T {
  return value;
}

let result1 = identity(10);    // T는 number로 추론됨
let result2 = identity("hello"); // T는 string으로 추론됨
```
여기서 T는 타입 매개변수이고, 이 함수는 입력값 value와 반환값의 타입이 같은 타입이 될 거라는 뜻

### 제네릭 함수의 활용
```typescript
function printArray<T>(arr: T[]): void {
  arr.forEach(item => console.log(item));
}

printArray([1, 2, 3]);       // 숫자 배열
printArray(["a", "b", "c"]); // 문자열 배열
```
T[]는 배열의 요소 타입이 나중에 결정되도록 만들어줌


## 제네릭 인터페이스
제네릭을 사용하면 인터페이스에서 타입을 나중에 지정할 수 있음
```typescript
interface Box<T> {
  value: T;
}

const numberBox: Box<number> = { value: 10 };
const stringBox: Box<string> = { value: "hello" };
```
Box<T>는 T라는 타입을 매개변수로 받아서, 나중에 number, string 등으로 타입을 지정할 수 있음

## 제네릭 클래스
클래스에서 제네릭을 사용하면, 클래스 내부에서 처리할 데이터 타입을 유연하게 정할 수 있음
```typescript
class Container<T> {
  private value: T;

  constructor(value: T) {
    this.value = value;
  }

  getValue(): T {
    return this.value;
  }
}

const numberContainer = new Container(42);
console.log(numberContainer.getValue()); // 42

const stringContainer = new Container("hello");
console.log(stringContainer.getValue()); // "hello"

```
```Container<T>```는 타입을 매개변수로 받아서 다양한 타입을 처리할 수 있다

## 제네릭을 활용한 제한
제네릭을 사용할 때, 제한을 걸어서 특정 타입만 받을 수 있게 할 수도 있다
### 제네릭에 제약 추가하기
```typescript
function merge<T extends object, U extends object>(obj1: T, obj2: U): T & U {
  return { ...obj1, ...obj2 };
}

const merged = merge({ name: "Alice" }, { age: 25 });
console.log(merged); // { name: "Alice", age: 25 }
```


T와 U는 객체 타입이어야 한다는 제약을 추가한 것

#  제네릭의 장점
1. 타입 안전성: 타입이 결정되지 않았을 때 발생할 수 있는 실수를 방지하고, 컴파일 타임에 오류를 잡을 수 있어요.

2. 유연성: 하나의 함수나 클래스에서 다양한 타입을 처리할 수 있어요.

3. 재사용성: 여러 곳에서 동일한 로직을 다양한 타입에 대해 사용할 수 있어요.

정리하자면 제네릭은 "타입을 나중에 지정할 수 있도록" 만들어주는 기능 그리고<br>
함수, 클래스, 인터페이스 등에서 제네릭을 사용하면 코드를 더 유연하게 만들 수 있으며 제네릭을 사용하면 타입 안전성도 높여주고, 재사용성과 가독성도 좋다~

