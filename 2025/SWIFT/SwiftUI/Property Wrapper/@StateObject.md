2025.07.28

## 1. `@ObservedObject`의 문제점
>`@ObservedObject`는 뷰가 다시 생성될 때마다 객체도 다시 연결됨

SwiftUI에서는 View가 자주 **재생성**되기 때문에<br>
`@ObservedObject`로 선언된 객체는 소유권이 없어서 매번 새로 생성되거나 연결됨

### 문제 상황 예시
```swift
struct ParentView: View {
    var body: some View {
        ChildView()  // 뷰가 상태 변화로 다시 그려질 때마다 새로운 ChildView() 생성
    }
}

struct ChildView: View {
    @ObservedObject var model = MyModel()  // 매번 새로 생성됨

    var body: some View {
        Text("\(model.count)")
    }
}
```
- `ChildView`가 다시 만들어질 때마다
- `MyModel()`도 새로 생성되기 때문에
- 이전 상태(`count`)가 초기화됨

## 2. 해결책: @StateObject
>뷰가 직접 생성한 ObservableObject의 생명주기를 관리해주는 속성

- 객체를 한 번만 만들고

- 뷰가 다시 그려져도 기존 객체를 유지
  
예시)
```swift
struct ChildView: View {
    @StateObject var model = MyModel()  // 한 번만 생성되고 계속 유지됨

    var body: some View {
        Text("\(model.count)")
    }
}
```


### @ObservedObject vs @StateObject 차이

|   |`@ObservedObject`|`@StateObject`
|:-:|:-:|:-:|
객체의 생성|외부에서 주입|내부에서 직접 생성
생명 주기|뷰가 다시 그려지면 객체도 새로 생성됨|객체는 한 번만 생성되고 유지됨
주로 쓰는 위치|자식 뷰 (외부 모델 전달받을 때)|모델을 처음 생성하는 뷰
상태 유지|안 됨 (재생성됨)|유지됨


### 정리 요약
Q|A
|:-:|:-:|
`@ObservedObject`의 문제점은?|뷰가 다시 생성될 때 객체도 새로 생성되어 상태가 초기화됨
왜 그런가요?|`@ObservedObject`는 객체를 직접 소유하지 않고, 외부에서 주입받기 때문
해결 방법은?|객체를 직접 생성해야 한다면 `@StateObject`를 사용해야 함
언제 사용하나요?|객체를 처음 생성하는 뷰에서는 `@StateObject`, 자식 뷰에서는 `@ObservedObject`