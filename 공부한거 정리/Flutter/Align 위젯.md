2025.12.22

# Align
부모가 주는 공간 안에서 자식 위젯을 원하는 위치에 딱 붙여서 배치하고 싶을때 Align 위젯을 사용하여 정렬할 수 있다고 합니다


## Align이 하는 것
### 1. 자식을 어디에 둘지 정한다(정렬)
`alignment:` 값으로 부모 영역 안에서 자식 위치를 결정합니다

- `Alignment.center` : 정중앙
- `Alignment.topLeft` : 왼쪽 위
- `Alignment.bottomRight` : 오른쪽 아래
- `Alignment(0, -1)` : 위쪽 중앙
- `Alignment(-1, 0)` : 왼쪽 중앙

Alignment 좌표는 `x: -1 ~ 1`, `y: -1 ~ 1`
- "x: -1 왼쪽, 0 가운데, 1오른쪽"
- "y: -1 위, 0 가운데, 1 아래"

예시)
```dart
Align(
    alignment: Alignment.topRight,
    child: Text("오른쪽 위"),
)
```

### 2.(옵션) Align 자체 크기를 조절할 수도 있다
`Align`은 기본적으로 부모가 주는 크기만큼 늘어나려는 성향이 있습니다<br>
그래서 "정렬할 공간"을 확보해놓고 그 안에서 자식을 옮기는 느낌이죠

근데 `widthFactor`, `heightFactor`를 주면 Align의 크기가 자식 기준으로 줄어듭니다

```dart
Align(
    alignment: Alignment.center,
    widthFactor: 2, // Align 너비 = 자식너비 * 2
    heightFactor: 2, // Align 높이 = 자식높이 * 2
    child: Container(width: 50, height: 50),
)
```
- factor를 안주면: 보통 부모 크기 꽉채움(가능한 만큼)
- factor를 주면: 자식 기준으로 "정렬 박스" 크기 결정됨

## 헷갈릴수있는거
### Align vs Center
- Center는 사실상 Align(alignment: Alignment.center) 랑 거의 같음
- 차이점은 Center은 무조건 가운데, Align은 어디든 가능 + factor도 있음
- 그래서 가운데 딱 정렬하는거면 Cneter위젯 쓰는게 빠를듯 합니다

### Align vs Positioned
- Positioned는 Stack 안에서 "좌표(top, left...)로 배치"
- Aligndms 부모 공간 안에서 정렬 (Stack 없어도 됨)

<br>

<hr>

<br>

2026.01.07

제가 공부하면서 헷갈릴 수 있을만한 내용을 강조하고 싶어서 추가합니다
일단 `Align`위젯은 적용한 위젯의 자식에 위치를 정해주는거지 자기 자신 즉 부모로 있는 위젯은 영향이 가지 않는 다는겁니다 자기 자신의 위젯에 Align을 적용하고 싶다면 또 다른 부모 위젯을 Align으로 감싸주면 됩니다
