2025.07.29

## `@EnvironmentObject`란
`@EnvironmentObject`는
>앱 전체에서 공유하는 전역 상태를 뷰 계층 어디서든 쉽게 접근할 수 있게 해주는 기능

예를 들어서

- 로그인 정보

- 테마 설정

- 사용자 설정값 등

전체 뷰에서 공유해야 하는 상태에 적합하죠


### 전제 조건
`@EnvironmentObject`를 사용하려면 반드시 다음 순서를 따라야 합니다:

1. `ObservableObject` 클래스를 만든다.

2. 앱 시작 지점에서 `.environmentObject()`로 주입한다.

3. 하위 뷰에서 `@EnvironmentObject`로 가져다 쓴다.

## 실전 예제

### 1. 데이터 모델 정의
```swift
import SwiftUI

class UserSettings: ObservableObject {
    @Published var username: String = "suho"
    @Published var isLoggedIn: Bool = false
}
```

- `ObservableObject` -> SwiftUI에게 "내 상태가 바뀌면 알려줄게"

- `@Published` -> 이 프로퍼티가 바뀌면 뷰가 다시 그려짐

### 2. App 시작 시 환경 객체로 주입
```swift
@main
struct MyApp: App {
    @StateObject var settings = UserSettings()  // 상태 소유는 여기서

    var body: some Scene {
        WindowGroup {
            ContentView()
                .environmentObject(settings)  // 환경 객체로 주입
        }
    }
}
```
- `@StateObject`: 객체를 직접 생성하고 생명주기를 App이 관리

- `.environmentObject(...)`: 이 객체를 앱 전체에 전달함


### 3. 하위 뷰 어디서든 사용
```swift
struct ContentView: View {
    @EnvironmentObject var settings: UserSettings  // 가져오기

    var body: some View {
        VStack {
            Text("Username: \(settings.username)")
            Button("Login") {
                settings.isLoggedIn = true
            }
        }
    }
}
```
- 뷰가 여러 번 재생성되어도 데이터는 유지되고

- 값이 바뀌면 자동으로 UI 갱신됨

## 왜 쓸까?
|||
|:-:|:-:|
@ObservedObject|상위 뷰에서 계속 전달해줘야 함 (번거로움)
@EnvironmentObject|앱 어디서든 접근 가능 (깔끔하고 유지보수 용이)



### 사용 예시
사용 상황|설명
로그인 상태|로그인/로그아웃 여부를 전역에서 사용
다크모드 / 테마 설정|뷰마다 테마 적용
유저 설정|글자 크기, 언어 설정 등
장바구니, 알림|앱 전역에서 공유되는 데이터

## 주의사항

|||
|:-:|:-:|
반드시 `.environmentObject()`로 주입해야 함|안 하면 런타임 크래시 발생
`@EnvironmentObject`는 생성하면 안 됨|무조건 외부에서 주입받아야 함
뷰 계층 내에서만 유효함|주입된 뷰 하위에서만 접근 가능


## 상태 관리 속성 비교

속성|생성 위치|공유 범위|주요 용도
|:-:|:-:|:-:|:-:|
@State|뷰 내부|❌|간단한 값 (int, bool) 상태
@StateObject|뷰 내부|❌|객체 상태 처음 생성 시
@ObservedObject|외부 주입|❌|상위 뷰에서 전달받을 때
@EnvironmentObject|외부 주입|✅ 앱 전역|전체 공유 데이터