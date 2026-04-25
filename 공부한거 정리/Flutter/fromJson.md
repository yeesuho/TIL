2026.04.23

벌써 곧 5월이 다가오네요<br>
정말 시간이 빨리 가는 것 같습니다...

오늘은 JSON 데이터를 객체로 바꿔주는 fromJson에 대해 알아볼건데요<br>

## JSON이 뭔데요
JSON이 뭔지 모르시는 분이 보실까봐 정리해드리겠습니다

JSON은 데이터를 주고받을 때 많이 쓰는 형식입니다

이름은 **JavaScript Object Notation**인데<br>
지금은 자바스크립트뿐 아니라 거의 모든 언어에서 다 씁니다

대충 서버가 앱에게 데이터 보낼 때, 앱이 서버에게 데이터 보낼 때, 파일에 데이터를 저장할 때 등 많이 쓰는 공통 데이터 표현 방식 입니다

## 왜 JSON 쓰는데요

음 예를 들어서 서버는 node, 앱은 Flutter, 웹은 React 이렇게 스택이 이렇게 되어 있다고 칩시다

그런데 서로 데이터를 주고받으려면
모두가 이해할 수 있는 **공통 언어 같은 형식**이 필요하겠죠

그게 JSON입니다

첨 보면 뭔 소리지 싶을 수 있는데요

```json
{
  "name": "Suho",
  "age": 18,
  "isStudent": true
}
```
예를 들어 서버가 이렇게 데이터를 보낸다고 해봅시다

이걸 보면 name은 "Suho", age는 18, isStudent는 true인건 다들 아시겠죠 이게 앞에 있는걸 key, 뒤에 변수 같은걸 value라고 하는데

그냥 쉽게 말해서 데이터를 담는 공용 박스 느낌입니다


## JSON의 생김새를 읽는 법
아까 JSON을 다시 봅시다

```json
{
  "name": "Suho",
  "age": 18,
  "isStudent": true
}
```
### 이거 읽는 방법

{ } : 하나의 객체 덩어리<br>
"name" : 키(key)<br>
"Suho" : 값(value)<br>

즉 JSON은 기본적으로<br>
키 : 값<br>
형태로 되어 있습니다

### 이걸 한 줄씩 보면

"name": "Suho" -> 이름은 Suho<br>
"age": 18 -> 나이는 18<br>
"isStudent": true -> 학생 여부는 true

이렇게 읽으시면 됩니다


## JSON에서 들어갈 수 있는 값 종류
이제 JSON 값에 들어갈 수 있는 타입을 알아보죠<br>
여러개 있습니다

### 문자열(String)
```json
"name": "Suho"
```
### 숫자(Number)
```json
"age": 18
```
### 참/거짓(Boolean)
```json
"isStudent": true
```
### 배열(List)
```json
"hobbies": ["coding", "music", "game"]
```
### 객체(Object)
```json
"address": {
  "city": "Seoul",
  "zipCode": "12345"
}
```
### null
```json
"phone": null
```

짜잔 다양하게 담을 수 있네요


2026.04.25

## 문자열 형태의 데이터

JSON은 왜 `문자열 형태의 데이터`라고 할까요

저도 알고나서 신기했는데요

JSON 자체는 우리가 눈으로 볼 때 이렇게 생겼죠
```json
{
  "name": "Suho",
  "age": 18
}
```
이걸 보면 객체처럼 보이는데 실제로 서버에서 앱으로 올 때는<br>
대부분 `텍스트(문자열)` 형태로 전달된답니다

### 이런식으로
```dart
'{"name":"Suho","age":18}'
```

겉모습은 객체처럼 생겼지만<br>
전송될 때는 문자들의 묶음으로 오는 겁니다

이건 Dart 입장에서는 그냥 문자열이죠<br>
아직 `user.name` 이런 식으로는 못 씁니다

Dart에서는 JSON 문자열을 보통 먼저 Map<String, dynamic>으로 바꿔줍니다

예를 들어 JSON이 이거라면

```json
{
  "name": "Suho",
  "age": 18
}
```

Dart에서는 대충 이렇게 다뤄집니다
```dart
Map<String, dynamic> json = {
  "name": "Suho",
  "age": 18,
};
```
여기서
- `"name"` 같은 키는 문자열이라 `String`
- 값은 `"Suho"`, `18`, `true`처럼 여러 타입일 수 있어서 `dynamic`

<br>

### 그럼 Map으로 쓰면 되지 왜 객체로 바꾸나요
사실 Map으로도 쓸 수는 있습니다

```dart
Map<String, dynamic> json = {
  "name": "Suho",
  "age": 18,
};
```

```dart
print(json["name"]);
print(json["age"]);
```
이렇게 써도는 됩니다<br>
문제는 점점 불편해진다는거죠


## Map만 쓰면 불편한 이유
### 1) 키 이름을 계속 문자열로 써야 함
```dart
json["name"]
json["age"]
json["isStudent"]
```
<br>

```dart 
json["nmae"]
```
만약에 이렇게 오타내면 찾기 어렵겠죠??


### 2) 어떤 데이터인지 한눈에 안 보임
`Map<String, dynamic>`은 너무 자유로워서
- 어떤 값이 꼭 있어야 하는지
- 타입이 뭔지
- 구조가 어떤지

코드만 보고 바로 파악하기 힘듭니다

### 3) 자동완성이 불편
객체를 쓰면
```dart
user.name
user.age
```
이렇게 알잘딱으로 자동완성이 잘 됩니다

근데 Map은
```dart
json["..."]
```
직접 써줘야하는 불편함이 있죠


### 4) 큰 프로젝트에서 관리가 힘들어짐
이 이유가 가장 클거 같은데요
예를 들어서 사용자 정보, 게시글 정보, 댓글 정보, 상품 정보가 다 Map이라면 코드가 금방 복잡해집니다

그래서 보통은 클래스로 정리합니다


## 객체로 바꾼다는 게 무슨 뜻이에요?
예를 들어 사용자 데이터를 다룬다고 해봅시다

그러면 이런 클래스를 만들 수 있죠
```dart
class User {
  final String name;
  final int age;
  final bool isStudent;

  User({
    required this.name,
    required this.age,
    required this.isStudent,
  });
}
```
- 이름
- 나이
- 학생 여부

를 가진 사용자 한 명을 표현하는 설계도면 같은 겁니다

사용할 때는 이렇게 쓸 수 있죠
```dart
User user = User(name: "Suho", age: 18, isStudent: true);

print(user.name);
print(user.age);
```

### 그런데 서버는 그런거 모름
서버는 저희가 만든 Dart의 `User` 클래스를 몰르겠죠

서버는 그냥 JSON만 보냅니다
```json
{
  "name": "Suho",
  "age": 18,
  "isStudent": true
}
```
근데 Flutter 앱 안에서는 이걸 User 객체로 쓰고 싶어

그럼 어떻게 해야겠어

JSON -> User 객체 변환해야겠죠

이걸 담당하는 게 `fromJson`입니다 와우


## fromJson은 정확히 뭐냐?

`fromJson`은 JSON 데이터를 받아서 객체를 만들어주는 함수 또는 생성자라고 합니다

예를 들어서

```dart
class User {
  final String name;
  final int age;
  final bool isStudent;

  User({
    required this.name,
    required this.age,
    required this.isStudent,
  });

  factory User.fromJson(Map<String, dynamic> json) {
    return User(
      name: json["name"],
      age: json["age"],
      isStudent: json["isStudent"],
    );
  }
}
```
이 코드를 보면<br>
`fromJson`은 JSON에서 값을 꺼내서<br>
`User(...)`를 만들어 주고 있습니다

```dart
User.fromJson(json)
```
이걸 실행하면 JSON이 User 객체가 되는 겁니다

## 흐름을 순서대로 보면
### 1) 서버가 JSON 문자열을 보냄
```dart
'{"name":"Suho","age":17,"isStudent":true}'
```

### 2) JSON 문자열을 Map으로 바꿈
이건 보통 `jsonDecode()`로 해줍니다
```dart
import 'dart:convert';

String responseBody = '{"name":"Suho","age":17,"isStudent":true}';

Map<String, dynamic> json = jsonDecode(responseBody);
```

이제 `json` 변수는 Map타입으로 이렇게 되겠죠
```dart
{
  "name": "Suho",
  "age": 17,
  "isStudent": true
}
```

### 3) Map을 User 객체로 바꿈
위에 만들었던 User객체를 사용해주면

fromJson 내부에서 User 객체 생성
```dart
return User(
  name: json['name'],
  age: json['age'],
  isStudent: json['isStudent'],
);
```
실제 값 대입해서
```dart
return User(
  name: "Suho",
  age: 18,
  isStudent: true,
);
```
User 객체 생성 완료됩니다

user 변수에 저장하면
```dart
User user = User.fromJson(json);
```

이제 `user` 변수에는 이런 객체가 들어 있게 됩니다
```dart
User(
  name: "Suho",
  age: 17,
  isStudent: true
)
```



### 4) 객체처럼 편하게 사용
```dart
print(user.name); // Suho
print(user.age);  // 18
```

## 정리
JSON은 데이터 전달용 형식이고<br>
앱에서는 보통 객체로 다루는 게 편하니까<br>
그 중간 변환 과정이 필요합니다

서버는 JSON으로 보내고 앱은 객체로 쓰고 싶음 이걸 도와주는게 `fromJson`
