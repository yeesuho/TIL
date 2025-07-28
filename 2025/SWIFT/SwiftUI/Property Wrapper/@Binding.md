2025.07.28

# `@Binding`
@Binding은 상위 뷰의 상태(@State)를 하위 뷰에서 변경할 수 있도록 연결해주는 역할을 합니다
>부모의 @State 값을 자식 뷰에서도 함께 보고 수정할 수 있게 해주는 다리 같은 역할

## 왜 필요할까
SwiftUI에서 @State는 해당 뷰 내부에서만 유효합니다
<br>
그래서 다른 뷰로 값을 직접 전달하고 수정하는 건 불가능하죠

```swift
struct ParentView: View {
    @State private var isOn = false
    
    var body: some View {
        ChildView(isOn: isOn)  // 에러 Bool을 그대로 전달하면 하위 뷰에서 수정 못함
    }
}

struct ChildView: View {
    var isOn: Bool  // 일반 Bool이라 수정 불가
    
    var body: some View {
        Toggle("스위치", isOn: $isOn)  // 에러 발생
    }
}
```

### 해결 방법: @Binding 사용
```swift
struct ParentView: View {
    @State private var isOn = false
    
    var body: some View {
        ChildView(isOn: $isOn)  // $ 붙이면 Binding으로 전달
    }
}

struct ChildView: View {
    @Binding var isOn: Bool  // 값을 공유받고 수정 가능
    
    var body: some View {
        Toggle("스위치", isOn: $isOn)  // 제대로 작동
    }
}
```

## Flow
1. 상위 뷰에서 `@State`로 변수 생성 <br>
`@State private var isOn = false`

2. 하위 뷰에 넘길 때는 `$isOn`처럼 달러($) 붙여서 넘김<br>
-> 이건 Binding 타입으로 변환

3. 하위 뷰에서는 `@Binding var isOn`으로 받아서<br>
-> 값을 읽고 쓰는 게 가능

## @State vs @Binding 차이
||`@State`|`@Binding`
|:-:|:-:|:-:|
정의 위치|해당 뷰 내부|외부에서 전달받음
값 수정 가능 여부|직접 가능	상위|뷰의 값을 수정
값의 소유자|자신이 주인|다른 뷰가 주인
주로 쓰는 위치|부모 뷰|자식 뷰

# 실제 예제
```swift
struct ParentView: View {
    @State private var isLiked = false
    
    var body: some View {
        VStack {
            Text(isLiked ? "❤️ 좋아요" : "🤍 안 좋아요")
            LikeButton(isLiked: $isLiked)  // 바인딩으로 전달
        }
    }
}

struct LikeButton: View {
    @Binding var isLiked: Bool  // 바인딩으로 받아서 제어
    
    var body: some View {
        Button(action: {
            isLiked.toggle()  // 부모 상태가 여기서도 바뀜
        }) {
            Text("좋아요 토글")
        }
    }
}
```

- 처음엔 "안 좋아요"

- 버튼 누르면 isLiked가 true가 되면서 "좋아요"로 바뀜

- 하위 뷰에서 값을 바꿨지만, 상위 뷰도 함께 반응함


# 주의할 점
주의사항|설명
|:-:|:-:|
`@Binding`은 직접 값을 가질 수 없음|항상 `@State`나 `@ObservedObject` 등의 상태에서 값을 받아와야 함
전달할 땐 `$` 기호 필수|`@State` 값을 넘길 땐 `$변수명`으로 바인딩 타입으로 변환
하위 뷰에서 `@Binding`을 수정하면 상위 뷰도 반영됨|상태가 연결되어 있으므로 데이터 흐름에 유의해야 함