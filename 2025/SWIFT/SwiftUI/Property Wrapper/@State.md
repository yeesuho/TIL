2025.07.28

# `@State`
`@State`는 뷰 내부에서 사용하는 값에 붙이는 속성입니다
<br>
이 값이 변하면 SwiftUI가 뷰를 자동으로 다시 그려줍니다

## 왜 필요할까
- SwiftUI는 데이터에 따라 UI가 바뀌는 방식(선언형 UI)

- 그런데 Swift의 일반 변수(var)는 값이 바뀌어도 UI가 바뀌지 않음

- 그래서 SwiftUI는 "이 값이 바뀌면 화면 다시 그려줘"<br>
라고 알려주는 `@State`라는 속성을 제공합니다

## 사용 예시
```swift
struct CounterView: View {
    @State private var count = 0  // <- @State로 선언

    var body: some View {
        VStack {
            Text("카운트: \(count)")
            Button("Plus Button") {
                count += 1  // 값이 바뀌면 화면이 자동으로 업데이트됨
            }
        }
    }
}
```
### Flow
1. 앱이 처음 실행되면 count는 0

2. 버튼 누르면 count가 1이 됨

3. SwiftUI가 자동으로 뷰를 다시 그림

4. Text("카운트: `누른 버튼 횟수만큼`") 증가된걸 볼 수 있음


## 특징과 주의점
특징|설명
|:-:|:-:|
뷰 내부 전용|@State는 해당 뷰 내부에서만 사용해야 함 (다른 뷰로 전달 불가)
구조체지만 값 유지됨|SwiftUI가 내부적으로 메모리 어딘가에 값을 저장해서, 뷰가 다시 그려져도 값을 잃지 않음
화면 자동 갱신|값이 바뀌면 화면이 자동으로 새로 그려짐 (re-render)
직접 접근 가능|그냥 일반 변수처럼 count += 1처럼 쓰면 됨


# 일반 변수와의 차이

### 일반 변수 일때
```swift
struct FailView: View {
    var count = 0

    var body: some View {
        VStack {
            Text("카운트: \(count)")
            Button("증가하기") {
                // count += 1  // 컴파일 오류 발생 struct는 immutable(불변성)이라 변경 불가
            }
        }
    }
}
```

### @State일 때
```swift
struct SuccessView: View {
    @State private var count = 0

    var body: some View {
        VStack {
            Text("카운트: \(count)")
            Button("증가하기") {
                count += 1  // 잘 동작함
            }
        }
    }
}
```


## 다른 View에 전달하고 싶다면
- @State 값은 다른 뷰에 직접 전달할 수 없음
- 대신 @Binding을 사용해야 함 (값을 공유하는 방법)