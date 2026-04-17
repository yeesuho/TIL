2026.04.18

InkWell 위젯은 처음 보면 그냥 GestureDetector랑 다를게 없어보이지만 사실 터치 처리 + 머티리얼 물결 효과(ink splash) + 하이라이트 효과를 함께 제공하는 위젯입니다 공식 문서에서도 InkWell은 반드시 Material 조상을 가져야 하고 잉크 반응은 실제로 그 Material 위에 그려진다고 설명해주네요

단순히 `터치만 감지`하는게 아니라 보이는 클릭 피드백까지 같이 주는 위젯이라고 생각하면 됩니다.

## 기본 형태

```dart
InkWell(
  onTap: () {
    print('클릭 됨');
  },
  child: Padding(
    padding: EdgeInsets.all(16),
    child: Text('클릭'),
  ),
)
```
- `child`가 화면에 보이는 내용
- `onTap`이 탭했을 때 실행되는 동작
- 누르면 child 영역 위에 물결 효과가 생김
하지만 여기서 이 코드가 제대로 보이려면 보통 상위에 `Material`이 있어야 합니다

```dart
Material(
  child: InkWell(
    onTap: () {
      print('클릭 됨');
    },
    child: Padding(
      padding: EdgeInsets.all(16),
      child: Text('클릭'),
    ),
  ),
)
```
왜냐면 잉크 효과는 `InkWell` 자신 위에 그려지는 게 아니라 배경이 되는 `Material` 위에 그려지기 때문입니다

## 왜 Material이 꼭 필요할까
공식 문서 기준으로 `InkWell`의 splash와 highlight는 **실제** `Material` **표면**에 그려진다고 되어 있습니다

그래서 Material이 없으면:
- 잉크 효과가 안 보일 수 있고
- 기대한 클릭 피드백이 사라질 수 있고
- assert(debugCheckHasMaterial(context)) 관련 문제가 생길 수 있습니다

<br>

- `InkWell` = 반응을 만드는 주체
- `Material` = 그 반응이 그려지는 바탕


## GestureDetector와 차이
많이 비교되는 게 GestureDetector인데요
### GestureDetector
- 탭, 더블탭, 드래그 같은 제스처 감지에 집중
- 시각적인 효과는 기본 제공 안 함

### InkWell
- 탭 같은 제스처 감지 가능
- 동시에 Material 스타일의 시각 효과 제공

<br>

효과 없이 입력만 받기 -> `GestureDetector`<br>
버튼처럼 보이게 클릭 피드백까지 주기 -> `InkWell`

공식 문서도 Material 앱에서는 GestureDetector 대신 InkWell을 사용할 수 있다고 설명합니다


## InkWell의 주요 콜백들
InkWell은 생각보다 이벤트가 많은데요

### onTap

가장 기본. 한 번 탭했을 때 실행

```dart
InkWell(
  onTap: () {
    print('클릭');
  },
  child: ...
)
```

### onDoubleTap
더블 클릭했을 때 실행
```dart
InkWell(
  onDoubleTap: () {
    print('더블 탭');
  },
  child: ...
)
```

### onLongPress
길게 눌렀을 때 실행
```dart
InkWell(
  onLongPress: () {
    print('길게 누름');
  },
  child: ...
)
```

### onTapDown
손가락이 닿는 순간 호출
```dart
InkWell(
  onTapDown: (details) {
    print('누르기 시작');
  },
  child: ...
)
```

### onTapUp
손가락을 뗐을 때 호출
```dart
InkWell(
  onTapUp: (details) {
    print('누르기 끝');
  },
  child: ...
)
```

### onTapCancel
탭이 중간에 취소되었을 때 호출

예를 들어 누르다가 손가락을 밖으로 빼면 취소될 수 있음
```dart
InkWell(
  onTapCancel: () {
    print('취소');
  },
  child: ...
)
```