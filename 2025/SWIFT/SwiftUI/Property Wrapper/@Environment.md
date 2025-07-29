2025.07.29

SwiftUI의 속성 래퍼 중 하나인 `@Environment`에 대해 알아보도록 하겠습니다

둘 다 Environment가 들어가서 헷갈릴 수 있지만 `@EnvironmentObject`와는 다른 개념입니다

`@Environment`는 SwiftUI가 제공하는 시스템 환경 값을 접근하는 데 사용되죠

# @Environment

> @Environment는 SwiftUI가 자동으로 제공하는 시스템/앱 관련 정보를 필요한 뷰에서 간편하게 꺼내 쓸 수 있게 해주는 속성 래퍼


예를 들면:
- 현재 다크 모드인지?

- 사용자의 지역(Locale)이 뭔지?

- 사용자가 선택한 글꼴 크기(Dynamic Type Size)는 어떤지?

- 접근성 설정이 활성화돼 있는지?

- 현재 뷰를 닫을 수 있는 dismiss 기능 등

우리는 `@Environment`로 필요할 때 가져다 쓰기만 하면 됩니다


### 대표적인 환경 값들
환경값 타입|설명
|:-:|:-:|
`colorScheme`|현재 다크모드인지 라이트모드인지
`locale`|사용자의 지역 (예: ko_KR, en_US)
`dismiss`|현재 뷰를 닫는 함수
`horizontalSizeClass / verticalSizeClass`|기기의 화면 사이즈 분류 (compact/regular)
`isEnabled`|버튼이나 뷰가 활성화되어 있는지
`scenePhase`|앱의 상태 (active, background 등)


### 언제 쓰면 좋을까?

상황|사용 예시
|:-:|:-:|
다크모드 대응 UI|`@Environment(\.colorScheme)` 사용해서 색상 조정
화면 닫기|`@Environment(\.dismiss)`로 현재 뷰 닫기
사용자의 언어에 따른 UI|`@Environment(\.locale)` 사용
뷰 크기/모양에 따라 UI 반응형 조절|`@Environment(\.horizontalSizeClass)` 등


## 기본 사용 예제

### 1. 현재 다크모드인지 확인하기
```swift
struct ContentView: View {
    @Environment(\.colorScheme) var colorScheme  // light 또는 dark

    var body: some View {
        Text("지금은 \(colorScheme == .dark ? "다크모드" : "라이트모드") 입니다")
    }
}
```

### 2. 현재 지역(Locale) 가져오기
```swift
struct ContentView: View {
    @Environment(\.locale) var locale  // 예: en_US, ko_KR

    var body: some View {
        Text("현재 언어: \(locale.identifier)")
    }
}
```

### 3. 현재 뷰를 닫는 dismiss 사용
```swift
struct ModalView: View {
    @Environment(\.dismiss) var dismiss

    var body: some View {
        Button("닫기") {
            dismiss()  // 현재 화면 닫기
        }
    }
}
```

## 어떻게 작동할까

SwiftUI 내부에는 EnvironmentValues라는 시스템이 있고
그 안에 수많은 값들이 미리 정의돼 있음

`@Environment(\.xxx)` 형태로 꺼내오면
SwiftUI가 그 뷰가 속한 **컨텍스트(Context)** 에 맞는 값을 넣어줌