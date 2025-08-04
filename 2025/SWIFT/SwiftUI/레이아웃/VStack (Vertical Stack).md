2025.08.04

## VStack (Vertical Stack)
>수직으로 뷰를 쌓는 스택

### 구조
```swift
VStack {
    Text("위")
    Text("아래")
    Image(systemName: "star")
}
```

### 결과
- 위에서 아래로 순서대로 정렬됨
```swift
위
↓
아래
↓
⭐️
```