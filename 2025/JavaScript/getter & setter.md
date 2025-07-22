2025.07.23

자바스크립트의 getter와 setter는 객체의 속성을 마치 변수처럼 보이지만 사실은 함수처럼 동작하게 만드는 기능<br>
속성에 접근하거나 값을 설정할 때 자동으로 특정 로직이 실행되도록 만들어줍니다

### 기본 개념
구분|설명
|:-:|:-:|
get|속성 읽을 때 실행되는 함수
set|속성 변경할 때 실행되는 함수

### 기본 사용
```js
const user = {
  firstName: "Suho",
  lastName: "Lee",
  
  get fullName() {
    return this.firstName + " " + this.lastName;
  },

  set fullName(value) {
    const parts = value.split(" ");
    this.firstName = parts[0];
    this.lastName = parts[1];
  }
};

console.log(user.fullName); // Suho Lee (get 호출)

user.fullName = "Suho Kim"; // set 호출
console.log(user.firstName); // Suho
console.log(user.lastName);  // Kim
```

- user.fullName은 변수처럼 보이지만, 사실 get 함수 실행 결과

- `user.fullName` = "값"은 set 함수가 자동 호출

- 내부 속성의 이름을 `firstName`, `lastName`으로 유지하면서 `fullName`이라는 인터페이스만 노출할 수 있음 -> 캡슐화



### 클래스에서의 getter / setter
```js
class Person {
  constructor(name) {
    this._name = name;
  }

  get name() {
    console.log("이름을 가져옵니다");
    return this._name;
  }

  set name(value) {
    console.log("이름을 설정합니다:", value);
    this._name = value;
  }
}

const p = new Person("Suho");
console.log(p.name);   // 이름을 가져옵니다 → Suho
p.name = "Minho";      // 이름을 설정합니다: Minho
console.log(p.name);   // Minho
```
>클래스에서는 주로 속성 앞에 `_`를 붙여 내부용 변수와 구분<br>`get name()`과 s`et name()`은 마치 `name`이라는 하나의 속성처럼 보이게 함.


### 사용 이유

사용 이유|설명
|:-:|:-:|
캡슐화|내부 데이터 보호 + 외부는 간단하게 인터페이스 제공
유효성 검사|set 안에서 조건 검사 가능
동적 계산|get으로 실시간 계산 결과 제공
디버깅|접근 시 로그 찍기, 변경 추적 등 가능