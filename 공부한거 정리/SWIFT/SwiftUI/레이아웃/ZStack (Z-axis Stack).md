2025.08.04

### ZStack (Z-axis Stack)
>Z축 방향으로 뷰를 겹쳐서 배치

### 구조
```swift
ZStack {
    Image("background")
    Text("앞에 있는 글자")
}
```

### 결과
- 이미지가 뒤에 깔리고, 글자가 앞에 겹쳐짐
```swift
[배경 이미지]
     ↑
  "앞에 있는 글자"
```