2025.06.01

# 아웃렛(Outlet) 변수

### 정의
UI 요소(예: 버튼, 레이블 등)의 속성이나 상태를 코드에서 제어하기 위해 연결하는 변수입니다


### 예시
```swift
@IBOutlet weak var myLabel: UILabel!
```
- ``@IBOutlet:`` Interface Builder와 연결된 변수임을 표시

- ``weak:`` 메모리 순환 참조 방지 (UI 요소는 보통 weak로 선언)

- ``UILabel:`` 연결된 UI 요소 타입

- ``myLabel:`` 내가 지은 변수 이름 (코드에서 사용됨)

>예: myLabel.text = "Hello!"로 레이블 텍스트 바꾸기

