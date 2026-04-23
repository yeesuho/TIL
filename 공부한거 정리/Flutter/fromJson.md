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
  "age": 17,
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
"age": 17 -> 나이는 17<br>
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
"age": 17
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

짜ㅈ잔다양하게 담을 수 있네요

