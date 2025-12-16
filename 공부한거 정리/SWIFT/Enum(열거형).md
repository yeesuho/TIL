2025.08.24

열거형 Enum, 풀네임은 Enumeration입니다

### 열거형 구문 (Enumeration Syntax)
열거형은 enum 키워드와 중괄호 안에 모든 정의를 위치시켜 나타냅니다
```swift
enum SomeEnumeration {
    // enumeration definition goes here
}
```
다음 예시는 나침반의 4개의 주요 포인트를 나타냅니다:
```swift
enum CompassPoint {
    case north
    case south
    case east
    case west
}
```
열거형 안에 정의된 값 (north, south, east, west)은 열거형 케이스 (enumeration cases) 입니다. 새로운 열거형 케이스를 나타내기 위해 case 키워드를 사용합니다.

## 기본 개념
열거형의 정의를 알고 가보자면
>같은 주제로 연관된 데이터들을 멤버로 구성하여 나타내는 자료형

입니다

무슨 말이냐면<br>
예를 들어서 날씨를 생각해보면 <br>
날씨는 맑음, 비, 눈, 흐림 같은 정해진 값들 중에서 하나라면<br>
그럴때 Swift에선 이렇게 enum을 쓸수 있습니다
```swift
enum Weather {
    case sunny   // 맑음
    case rain    // 비
    case snow    // 눈
    case cloudy  // 흐림
}
```
그리고 이렇게 사용 가능하죠
```swift
var todayWeather = Weather.sunny
```

#### 또한 switch문으로 어떤 날씨인지 쉽게 확인할 수 있습니다
```swift
switch todayWeather {
case .sunny:
    print("맑은 날이에요")
case .rain:
    print("비가 와요")
case .snow:
    print("눈이 와요")
case .cloudy:
    print("흐려요")
}
```
switch를 쓸 때는 모든 경우를 빠짐없이 써줘야 합니다 (안 그러면 에러가 날 수 있음)


## 사용 예시 파헤치기
예시를 더 보자면 에러를 처리할 때 왜 에러가 났는지 설명도 함께 넣고 싶다고 치면
```swift
enum AppError {
    case networkError(message: String)
    case serverError(code: Int)
}
```

```swift
let error = AppError.networkError(message: "인터넷이 끊겼어요")

switch error {
case .networkError(let msg):
    print("네트워크 에러: \(msg)")
case .serverError(let code):
    print("서버 에러 코드: \(code)")
}
```
이렇게 enum이지만 값을 붙여서 쓸 수 있죠<br> 이걸 "연관 값"이라고 합니다


#### 정해진 숫자나 문자열이랑 연결할 수도 있음
예를 들어 요일
```swift
enum Day: Int {
    case monday = 1
    case tuesday
    case wednesday
    case thursday
    case friday
    case saturday
    case sunday
}
```
```swift
let today = Day(rawValue: 5) // friday
```

### 간단히 정리
개념|설명|예시
|:-:|:-:|:-:|
enum|정해진 선택지 중 하나|`Weather.sunny`
switch|어떤 값인지 확인|`switch todayWeather { ... }`
연관값|선택지에 정보 붙이기|`.networkError(message: "오류")`
rawValue|숫자나 문자열 연결|`Day(rawValue: 1)` → monday