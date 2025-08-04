2025.08.04

## 스택(Stack) 기본 개념

SwiftUI는 뷰를 배치할 때 좌표를 직접 지정하는 대신<br>
**스택(Stack)** 이라는 레이아웃 도구를 써서 정렬 방식을 지정합니다

그중에는 VStack(수직으로 정렬), HStack(수평으로 정렬), ZStack(Z축으로 정렬)이 있습니다


### 중첩 사용도 가능
```swift
VStack {
    Text("제목")
    HStack {
        Text("왼쪽")
        Spacer()
        Text("오른쪽")
    }
}
```

### 정렬
```swift
VStack(alignment: .leading) {
    Text("이름")
    Text("이수호")
}
```
- 두 텍스트가 왼쪽 정렬됨

### Text 정렬
```swift
Text("Hello, Suho!")
    .frame(width: 200, alignment: .leading)
```


## 함께 기억하면 좋은 정렬 속성들

정렬 속성|설명
|:-:|:-:|
`.leading`|왼쪽 정렬 (언어 기준 시작 방향)
`.trailing`|오른쪽 정렬
`.center`|가운데 정렬
`.top / .bottom`|위쪽 / 아래쪽 정렬 (세로 방향)