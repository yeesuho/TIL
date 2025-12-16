2025.07.28

## Property Wrapper(프로퍼티 래퍼)
Property Wrapper(프로퍼티 래퍼)는 변수에 특정 기능을 부여하거나 동작을 자동화하는 Swift의 문법 기능입니다<br>
SwiftUI에서는 이 기능을 활용해서 상태 관리, 데이터 바인딩, 의존성 주입 등을 간단하게 구현할 수 있죠


## SwiftUI의 대표적인 Property Wrapper
래퍼|설명
|:-:|:-:|
@State|View 내부에서 값 변경을 감지하고 화면을 업데이트하게 해줌. (내부 상태)
@Binding|부모 뷰의 @State 값을 하위 뷰와 연결하여 값을 공유함.
@ObservedObject|외부에서 전달된 객체의 변화를 뷰가 관찰함.
@StateObject|뷰 내부에서 직접 생성하고 관리하는 객체. SwiftUI가 생명 주기를 관리함.
@EnvironmentObject|앱 전체에서 공유되는 전역 상태를 사용함.
@Environment|시스템 또는 SwiftUI에서 제공하는 환경 값 접근 (예: 다크모드, locale 등).