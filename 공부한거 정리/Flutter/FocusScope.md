2026.01.06

휴 TIL 쓰기 시작한게 2025인데 벌써 2026입니다 <br>
새로 태어난 마음가짐으로 열심히 살아보겠습니다

오늘 적을 내용은 아주 기본적이고 쉬운거지만 그런걸 쓰는게 TIL 아닐까요  

자 그럼 본론으로 TextField를 사용할때 TextField가 아닌 다른 곳을 터치해서 키보드를 내리게 하고 싶은 경우가 있잖아요 그걸 어떻게 하는지 한번 알아보겠습니다 그리고 자주 겪는 문제도 풀어볼게요

## Focus/FocusNode/FocusScope
Flutter에서 키보드는 TextField가 키보드를 띄운다기 보다는 어떤 위젯이 `focus`를 가지고 있으면 시스템이 "아 입력 중이구나" 이러고 키보드를 올려주는 구조입니다

### Focus
- 지금 입력을 받는 대상이 누구? 를 의미합니다
- 예를 들어서 TextField를 탭하면 그 TextField가 포커스를 가져감 -> 키보드가 올라옴

### FocusNode
- 포커스를 추적/제어하는 객체
- TextField는 내부적으로 FocusNode를 갖거나 우리가 직접 넣을 수 있습니다
- `이TextField에 포커스 줘/빼줘` 같은걸 FocusNode로 제어 가능
```dart
final node = FocusNode();
// node.requestFocus(); // 포커스 주기
// node.unfocus(); // 포커스 빼기
```

### FocusScope
- 여러 FocusNode를 `그룹으로 관리` 하는 관리자 같은 느낌
- 화면(트리) 안에는 FocusScope가 존재하고 그안에는 여러 TextField의 FocusNode 들이 있습니다 
- 그래서 `FocusScope.of(context)`는 `이 context 위치 기준으로 가장 가까운 FocusScope 찾아줘` 라는 뜻입니다

### flutter에서 키보드를 내리는 가장 표준적인 방법(국룰)
```dart
FocusScope.of(context).unfocus();
```
이 한줄을 쉽게 설명하자면
1. 현재 context 기준으로 FocusScope(관리자)를 찾고
2. 그 관리자가 잡고 있는 현재 포커스를 해제
3. 포커스를 가진 입력 위젯이 없어짐 -> 시스템이 키보드를 내림
즉 키보드 자체를 "닫아라" 명령하는건 아니고 포커스를 없애서 키보드가 내려갈 수 밖에 없게 만드는 방식입니다

<br>

## onTap 에러(void vs Function)
제가 실제로 했던 실수인데 onTap에 함수를 넣다보면 즉시 실행 함수를 넣는 실수를 할때가 많습니다

예를 들어서 onTap은 타입이 이런 느낌입니다
```dart
final VoidCallback? onTap; // = void Function()?
```
즉 `"나중에 실행할 함수"`를 받아야하죠

#### 틀린코드
```dart
onTap: FocusScope.of(context).unfocus(),
```
근데 여기서 unfocus에 ()를 붙이면 즉시 실행이 되기 때문에
빌드 되는 순간 unfocus가 실행되고 실행 결과는 void(값 없음) 이런 상황이 발생합니다

#### 맞는 코드
```dart
onTap: () {
    FocusScope.of(context).unfocus()
},

onTap: () => FocusScope.of(context).unfocus(),
```
하지만 위에 두 코드처럼 익명함수를 사용하면 "탭하면 실행할게유" 라는 함수 자체를 넘기는거라 사용할 수 있게 됩니다


<br>

### 그리고 한가지 더 Dialog에서 사용하는법
이것도 제가 기능대회 문제를 풀다가 알게된건데 일반적으론 그냥 제일 상위 Scaffold를 `GestureDetector`로 감싸서 onTap에 FocusScope ~ unscope~ 이런식으로 하면 focus가 풀리게 되는데요 하지만 show Dialog는 얘기가 다릅니다

여기서 핵심은 Dialog는 `다른 레이어(Overlay)` 위에 올라간다는 겁니다
- Scaffold에 GestureDetector를 깔아도
- Dialog가 떠 있는 동안엔 터치가 Dialog 레이어에서 소비돼버려서
- 뒤에 있는 Scaffold의 GestureDetector까지 이벤트가 내려가지 않습니다

그래서 Dialog 내부에서도 터치를 잡아서 unfocus 해줘야 한답니다 하핫

```dart
showDialog(
    context: context,
    builder: (context) {
        return GestureDetector(
            behavior: HitTestBehavior.opaque, // 빈 곳도 탭 인식되게 해줌
            onTap: () => FocusScope.of(context).unfocus(),
            child: Dialog(
                child: ...
            ),
        );
    },
);
```
여기서 `behavior: HitTestBehavior.opaque` 를 써야하는 이유는 Dialog 안에서 투명한 빈공간을 탭했을때 GestureDetector가 터치를 못 잡는 경우가 있어서 그걸 확실히 잡으려면 `opaque`로 해두는게 안정적입니다

<br>

### 진짜 마지막으로 실전에서 가장 많이 쓰는 패턴
```dart
GestureDetector(
    behavior: HitTestBehavior.translucent,
    onTap: () => FocusScope.of(context).unfocus(),
    child: Scaffold(
        body: ...
    ),
);
```
translucent도 자주 쓴다고 합니다 (투명 영역도 탭 잡기)

2026.01.08
더 간단한 방법이 있어서 내용을 추가합니다
버튼에 out