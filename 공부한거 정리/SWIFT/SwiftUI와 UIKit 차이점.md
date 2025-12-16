2025.06.05

SwiftUI와 UIKit은 둘 다 iOS 앱의 사용자 인터페이스(UI)를 만들기 위한 프레임워크입니다<br>
하지만 접근 방식, 코드 스타일, 동작 방식 등에서 큰 차이가 있습니다<br>
개념적인 차이, 코드 스타일, 장/단점, 그리고 언제 어떤 걸 쓰는 게 좋을지 간단하게 정리해볼게요

### 기본 개념 차이

||SwiftUI|UIKit
|:-:|:-:|:-:|
등장 시기|2019년 (iOS 13)|2008년 (iOS 2)
방식|선언형(Declarative)|명령형(Imperative)
UI 구성 방식|어떻게 보일지 선언|무엇을 어떻게 할지 직접 제어
상태 관리|@State, @Binding, ObservableObject|	뷰 컨트롤러에서 직접 관리
미리보기|실시간 Preview 지원|시뮬레이터나 기기에서 실행해야 확인 가능
레이아웃 시스템|VStack, HStack, ZStack|AutoLayout, Constraints 사용

<br>

### 코드 스타일 차이
#### SwiftUI
```swift
import SwiftUI

struct ContentView: View {
    @State private var counter = 0

    var body: some View {
        VStack {
            Text("Counter: \(counter)")
            Button("Increase") {
                counter += 1
            }
        }
    }
}
```

<br>

UIKit
```swift
import UIKit

class ViewController: UIViewController {
    var counter = 0
    let label = UILabel()
    let button = UIButton()

    override func viewDidLoad() {
        super.viewDidLoad()

        label.text = "Counter: \(counter)"
        label.frame = CGRect(x: 100, y: 100, width: 200, height: 50)
        view.addSubview(label)

        button.setTitle("Increase", for: .normal)
        button.frame = CGRect(x: 100, y: 200, width: 100, height: 50)
        button.addTarget(self, action: #selector(increaseCounter), for: .touchUpInside)
        view.addSubview(button)
    }

    @objc func increaseCounter() {
        counter += 1
        label.text = "Counter: \(counter)"
    }
}
```

## 장단점 비교
### SwiftUI
#### 장점
- 코드 간결, 생산성↑

- 다크 모드, 접근성 등 시스템 기능 통합이 쉬움

- 실시간 Preview로 빠른 개발

- 재사용 가능한 UI 컴포넌트 제작이 쉬움

#### 단점
- iOS 13 이상에서만 지원 (호환성 문제)

- 아직 UIKit보다 기능 제한이 있음

- 복잡한 UI나 커스터마이징은 어려움

- 디버깅 도구와 생태계가 UIKit만큼 완성되지 않음
- 
<br>

### UIKit
#### 장점
- 오래된 프레임워크로 안정적

- 복잡한 UI/애니메이션 등 세세한 컨트롤 가능

- 다양한 오픈소스/라이브러리 생태계

- 많은 튜토리얼과 학습 자료

#### 단점
- 코드 양 많고 복잡함

- 상태 관리, 다크 모드 대응이 번거로움

- 실시간 미리보기 없음

## 언제 뭘 쓰는게 더 좋을까?

상황|추천
|:-:|:-:|
iOS 13 이상, 새 앱 개발|SwiftUI 추천 (간단하고 빠름)
복잡한 커스텀 UI, 애니메이션, iOS 12 이하 호환|UIKit
SwiftUI에 없는 기능을 써야 할 때|UIKit과 SwiftUI를 혼합 (가능함)
입문자이고 최신 개발 방식으로 배우고 싶을 때|SwiftUI 시작 추천

>그렇다고 무조건 같이 쓰는게 좋은것은 아님

### 그럼 이렇게 생각할 수 있음
왜 무조건 같이 쓰는게 좋은건 아닌가여??<br>

### 문제 1. 복잡도 증가
SwiftUI와 UIKit을 동시에 쓰면 코드 구조가 복잡해짐
- SwiftUI는 선언형, UIKit은 명령형이라 개발 방식 자체가 달라서 섞으면 정신없어짐
- 관리할 게 두 배: UIViewController 생명주기 vs SwiftUI의 상태 바인딩 등

### 문제 2. 퍼포먼스 문제 가능성
SwiftUI <-> UIKit 간 호환 레이어(UIHostingController, UIViewRepresentable 등) 는 성능 손실 가능
- 앱이 자주 뷰 전환하거나, UIKit 뷰를 자주 업데이트하면 오버헤드 생김
- SwiftUI 안에 UIKit 넣었다가 그 안에 또 SwiftUI 넣고… 복잡하면 느려질 수 있음


### 문제 3. 코드 재사용성이 떨어질 수 있음
한 화면은 SwiftUI, 다른 화면은 UIKit이면 공통 UI/로직을 나누기 어려움
- 예: 공통 버튼 스타일을 SwiftUI용으로 한 번, UIKit용으로 또 만들어야 함

- 똑같은 기능인데 코드 두 번 작성해야 하는 상황 생김

>결론적으로 같이 쓸 때 좋은 건	SwiftUI에서 부족한 기능을 UIKit으로 보완할 때 이고 아무 이유 없이 무조건 같이 쓰는 건 복잡하고 비효율적일 수 있습니다
