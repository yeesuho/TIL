2025.03.29


## 먼저 type을 알아볼까나
사용자 정의 타입(User-Defined Type) => 사용자가 직접 새로운 타입을 만들 수 있음

type 키워드로 타입 만들기 (Type Alias)
```typescript
type UserID = string | number;

let id1: UserID = 123;   // 가능 (숫자)
let id2: UserID = "abc"; // 가능 (문자열)
// let id3: UserID = true; // 오류: (boolean은 안 됨)
```
UserID는 string 또는 number 둘 중 하나만 가능하도록 만든 타입임

<br>

## interface로 타입 만들기 (객체 타입 정의)
interface는 객체의 구조를 정의하는 기능<br>
쉽게 말해서, interface는 **객체(데이터 구조)** 가 특정한 형태를 가지도록 "규칙"을 정하는 것<br>
이 규칙을 따르면 코드가 더 안전해지고, 실수도 줄일 수 있음
```typescript
interface User {
  id: number;
  name: string;
  isAdmin?: boolean; // 옵셔널 (있어도 되고 없어도 됨)
}

const user1: User = { id: 1, name: "Alice" }; // 가능
const user2: User = { id: 2, name: "Bob", isAdmin: true }; // 가능
// const user3: User = { id: 3 }; // 오류: (name이 없음)
```
User 인터페이스를 만들면, id랑 name이 꼭 필요하고 isAdmin은 선택 가능

<br>

# type과 interface
interface vs type<br>
차이점: <br>
|특징|interface|type|
|:----:|:------:|:----:|
확장 가능|extends로 확장 가능|```&```(intersection)으로 확장 가능
선언 병합|가능 (interface 여러 번 선언하면 병합됨)|불가능
사용 대상|객체, 클래스|모든 타입 가능 (유니온, 튜플 등)

### 객체 타입 정의
type과 interface 모두 객체 타입을 정의할 수 있음
```typescript
type Person = { name: string, age: number };
interface User { name: string, age: number };
```

### 유니온(```|```) 타입 사용
type에서는 유니온 타입(|)을 사용해서 여러 타입을 결합할 수 있음
```typescript
type ID = string | number;
```
<hr>
interface는 유니온 타입을 사용할 수 없고 대신 인터페이스를 확장
(extends)하거나 조합(&)할 수 있음

### 튜플 정의
type은 튜플 타입을 정의할 수 있지만
```typescript
type Point = [number, number];
```
interface는 튜플을 정의할 수 없고 객체 타입만 다룰 수 있음

### 확장(상속)
type은 ```&``` 연산자로 타입을 확장할 수 있고
```typescript
type Employee = Person & { job: string };
```
interface는 extends 키워드로 확장할 수 있음
```typescript
interface Admin extends User { isAdmin: true }
```


### 가독성 & 직관성
**type** 은 단순하고 간단한 타입을 정의할 때 좋고, <br>
**interface** 는 객체 구조를 정의할 때 직관적이고 명확