2026.01.06

# Stack 위젯
Stack은 위젯을 z축을 기준으로 순서대로 배치할 수 있는 위젯입니다<br>
Stack 내에 자식들 `children:[]` 코드 내에서 가장 위에 존재하는 위젯이 화면에선 가장 밑에 쌓이게 됩니다 

자료구조의 Stack과 같은 내용인데 쉽게 말하자면 동전 지갑 같은겁니다 예를들어 먼저 들어간 동전은 밑에 쌓이죠 `Stack 위젯`에서도 위에서 말했다 싶이 밑에서부터 차곡차곡 쌓이게 됩니다

```dart
Stack(
    children: [
        Container( 
            // 화면을 꽉차지 해줌
            width: MediaQuery.of(context).size.width, 
            height: MediaQuery.of(context).size.height,
            color: Colors.blue,
        ),
        Cneter( // 보기 좋게 중앙 정렬
            child: Container(
                width: 50,
                height: 50,
                color: Colors.red,
            )
        )
    ]
)
```
이 코드는 밑에 화면을 꽉 차지 하는 파란색 Container가 있게 되고 그 Container 위에 빨간색 width: 50, height50 사이즈의 Container가 중앙에 정렬될겁니다 이제 좀 이해가 될까요??

<br>

## 그럼 Positioned은 뭔데요
Postitioned위젯은 Align 위젯과 비슷한데 Stack 내에서만 쓸수있는 위젯입니다 <br> 위젯을 여러 개 쌓을 때 세세한 위치 조정이 필요하다면 Positioned를 사용할 수 있습니다<br>
물론 Postitioned위젯을 모른다고해서 하늘나라 가는건 아니지만 Stack 내에서 위젯을 정렬하는데 매우 유용하기 때문에 아는게 이득입니다


## Positioned 위젯이 필요한 이유
그냥 Stack을 사용하면 
- 기본 정렬(alignment)에 따라 겹치거나
- 각 위젯이 자기 크기대로 배치됩니다
- 근데 예를 들어서 왼쪽(left)에서 20lp 위(top)에서 40lp 이런식으로 딱 정확한 위치에 지정하고 싶으면 Positioned를 쓰면 됩니다

## Positioned 기본 구조
```dart
Stack(
    children: [
        Positioned(
            left: 20,
            top: 40,
            child: Text("하이"),
        ),
    ],
),
```

여기서 left/top/right/bottom은 Stack의 바깥 경계(= Stack의 크기) 를 기준으로 잡힙니다

##  left/top/right/bottom은 “거리”

left: 20 -> 왼쪽 경계에서 20lp 떨어져라<br>
top: 40 -> 위쪽 경계에서 40lp 떨어져라<br>
right: 10 -> 오른쪽 경계에서 10lp 떨어져라<br>
bottom: 0 -> 아래쪽 경계에 딱 붙어라

물론 -(마이너스)도 됩니다

## width/height까지 주면 “크기 고정”

Positioned는 위치뿐 아니라 크기도 고정할 수 있습니다

1번 예시: left + top + width + height
```dart
Positioned(
  left: 20,
  top: 20,
  width: 120,
  height: 50,
  child: Container(color: Colors.red),
)
```
>(x축으로 20, y축으로 -20[top이라서 밑으로 내려감])에 120x50 크기 박아버림

2번 예시: left + right 같이 쓰면 “양쪽으로 늘어나기”
```dart
Positioned(
  left: 16,
  right: 16,
  top: 20,
  child: Container(height: 50, color: Colors.blue),
)
```


>좌우가 16px씩 비고, 가로는 남은 공간만큼 자동으로 쭉 늘어남 (이때 width를 직접 주면 충돌 날 수 있어)

## 자주 하는 실수
### Stack 밖에서 Positioned 쓰면 나는 에러
이건 Flutter를 처음 배우거나 개똥벌레가 아닌 이상 하지 않는 실수긴 한데 중요하긴 하니까 넣었습니다<br>
암튼 Positioned는 Stack 전용 ParentData가 필요해서
Column, Row 같은데 넣으면 이런 류 에러가 납니다:

>“Incorrect use of ParentDataWidget”

>“Positioned widgets must be placed inside a Stack”

### left/right/width를 동시에 주기

#### 가로 방향에서 규칙이 있습니다:
(left + width)<br>
(right + width)<br>
(left + right)<br>
(left + right + width) (모순이라서 안됨)

#### 세로도 똑같이:
(top + height)<br>
(bottom + height)<br>
(top + bottom)<br>
(top + bottom + height)

## Positioned vs Align 차이
이건 Align 내용 쓸때도 쓰긴했지만 여긴 좀더 자세하게 쓰겠습니다
둘 다 자식 위치 잡을 때 쓰지만 느낌이 다릅니다
Positioned는 거리로 고정해서 “왼쪽에서 10, 아래에서 30” 이런식으로
정확한 픽셀 위치 기반이고

Align은 정렬로 배치해서
```dart
Align(
  alignment: Alignment.bottomRight,
  child: ...
)
```
Align: “오른쪽 아래에 붙여” <br> 이렇게 반응형/비율 기반 느낌입니다

정확한 좌표 -> Positioned(Stack에서만)<br>
정렬 느낌 -> Align

## Positioned.fill / Positioned.fromRect
### Positioned.fill

Stack 영역을 꽉 채우고 싶을 때 사용합니다
```
Positioned.fill(
  child: Container(color: Colors.black26),
)
```
### Positioned.fill + padding처럼 쓰기
```dart
Positioned.fill(
  left: 16,
  right: 16,
  top: 20,
  bottom: 20,
  child: ...
)
```
-> 가장자리에서 일정 거리 두고 꽉 채우기

### Positioned.fromRect
Positioned.fromRect는 “Stack 안에서 child를 ‘사각형(Rect)’ 하나로 위치+크기까지 한 번에 지정” 하는 생성자입니다
- left/top/right/bottom으로 하나하나 거리 주는 대신
- Rect(좌표 + 폭/높이) 를 딱 주면 그 Rect에 맞춰 배치해줍니다

#### 뭐로 이루어져 있냐?
Rect는 사각형 영역이고 대표적으로 이렇게 만들 수 있습니다:
1) Rect.fromLTWH(left, top, width, height)
- 가장 많이 씀
- Left, Top, Width, Height
```dart
final rect = Rect.fromLTWH(20, 40, 120, 60);
```
2) Rect.fromPoints(Offset a, Offset b)
- 두 점(좌상단/우하단 비슷한 느낌)으로 Rect 만들기
```dart
final rect = Rect.fromPoints(Offset(20, 40), Offset(140, 100));
```

#### 기본 사용 예시
```dart
Stack(
  children: [
    Positioned.fromRect(
      rect: Rect.fromLTWH(20, 40, 120, 60),
      child: Container(color: Colors.red),
    ),
  ],
)
```
이건 아래랑 완전 같은 의미입니다
```dart
Positioned(
  left: 20,
  top: 40,
  width: 120,
  height: 60,
  child: Container(color: Colors.red),
)
```


## 실전 UI에서 자주 나오는 패턴
### 카드 위에 뱃지 올리기
```dart
Stack(
  children: [
    Card(child: ...),
    Positioned(
      top: 8,
      right: 8,
      child: Container(
        padding: EdgeInsets.symmetric(horizontal: 8, vertical: 4),
        decoration: BoxDecoration(
          color: Colors.red,
          borderRadius: BorderRadius.circular(12),
        ),
        child: Text("NEW", style: TextStyle(color: Colors.white)),
      ),
    ),
  ],
)
```

### 배경 이미지 + 글자 오버레이
```dart
Stack(
  children: [
    Image.asset("bg.jpg", fit: BoxFit.cover, width: double.infinity),
    Positioned(
      left: 16,
      bottom: 16,
      child: Text("Hello", style: TextStyle(fontSize: 24, color: Colors.white)),
    ),
  ],
)
```