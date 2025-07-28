2025.07.28

# Observable 3총사
`ObservableObject` 프로토콜<br>
`@Published` 속성 래퍼<br>
`@ObservedObject` 프로퍼티 래퍼

SwiftUI에서 데이터 바인딩과 UI 자동 갱신을 가능하게 해주는 핵심 조합입니다

## 1. ObservableObject – 변화를 알려주는 클래스
### 역할
`ObservableObject`는 SwiftUI에<br>
>"나 상태가 바뀌면 알려줄게"<br>라고 선언하는 클래스입니다

이 프로토콜을 채택한 클래스는
@Published 속성이 변경될 때 자동으로 알림을 보낼 수 있죠

```swift
import SwiftUI
import Combine

class Counter: ObservableObject {
    @Published var count = 0
}
```
- `ObservableObject`: 이걸 채택해야 SwiftUI가 상태를 감지할 수 있음

- 하지만 이것만으론 화면 업데이트가 안됨<br> 함께 @Published, @ObservedObject가 필요함


## 2. @Published – 값 변경을 감지하게 만듦
### 역할
`@Published`는 클래스의 속성에 붙여서
> "이 속성이 바뀌면 나를 지켜보는 뷰에 알려줘" <br>라고 하는 래퍼입니다

```swift
class Counter: ObservableObject {
    @Published var count = 0  // 변경 시 뷰에게 알림
}
```
- 이 속성이 바뀌면 자동으로 SwiftUI 뷰에 업데이트 신호가 감

- `@Published`가 붙지 않으면 값이 바뀌어도 뷰가 모름

### 주의
- `@Published`는 `ObservableObject` 클래스 안에서만 써야 함

- 구조체나 일반 클래스에는 단독으로 의미 없음

## 3. @ObservedObject – 객체를 관찰하고 UI를 갱신함
### 역할
SwiftUI의 뷰에서 `ObservableObject`를 감지하려면

> "이 객체를 관찰해서 값이 바뀌면 내 화면을 다시 그려줘" <br>라는 의미로 @ObservedObject를 사용합니다

```swift
struct CounterView: View {
    @ObservedObject var counter: Counter
    
    var body: some View {
        VStack {
            Text("Count: \(counter.count)")
            Button("Increase") {
                counter.count += 1
            }
        }
    }
}
```
- `@ObservedObject`는 외부에서 전달된 모델을 구독(subscribe) 해

- `@Published` 값이 바뀌면 뷰가 다시 그려짐 (자동 반응)

## Flow
```css
[ @Published ]
     ⬇️ 값 변경 감지
[ ObservableObject ]
     ⬇️ 알림 전파
[ @ObservedObject ]
     ⬇️ SwiftUI 뷰 리렌더링
[ UI 자동 업데이트 ]
```


### 실전 예시
```swift 
// 모델 클래스 정의
class CounterModel: ObservableObject {
    @Published var count = 0
}

// View에서 관찰
struct ContentView: View {
    @ObservedObject var model = CounterModel()  // 또는 외부에서 주입받기
    
    var body: some View {
        VStack {
            Text("Count: \(model.count)")
            Button("증가") {
                model.count += 1  // 자동으로 화면 갱신됨
            }
        }
    }
}
```


## 요약

이름|역할|어디에 쓰나
|:-:|:-:|:-:|
`ObservableObject`|클래스가 상태 변경을 알릴 수 있게 함|모델 클래스 선언 시
`@Published`|속성의 값 변경을 감지하고 알림 전송|모델 클래스 속성
`@ObservedObject`|모델 객체를 관찰하여 화면 자동 업데이트|SwiftUI 뷰 내부


`@State`는 **값 타입(value type)** 인 Int, Bool, String, Array, Struct 등의 값이 바뀌면 SwiftUI가 화면을 자동으로 리렌더링 (re-render) 해주지만<br>
**클래스(참조 타입, reference type)** 의 내부 값 변화를 감지하지 못함

그래서 SwiftUI는 클래스의 속성 변화까지 감지하려면<br>
-> `@Published`, `ObservableObject`, `@ObservedObject` 같은 **Observable 삼총사**를 써야 합니더