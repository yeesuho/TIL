2025.12.27

StatefulWidget이 정확히 뭐고, 생명주기 메서드들이 언제/왜 호출되는지까지 정리해보긌습니다

# StatefulWidget이란?
StatefulWidget = “위젯은 불변(immutable)이고, 변하는 값은 State 객체가 들고 있는 구조”

StatefulWidget 인스턴스 자체는 Stateless처럼 불변입니다

실제로 화면이 바뀌는 “상태”는 State<T> 안에 저장되죠

화면 갱신은 setState()를 통해 트리의 해당 부분을 rebuild 하면서 일어난답니다


### 구조
```
StatefulWidget (설정값, 불변)
    |
    -> State (변하는 값, 생명주기, setState)
```


그럼 이런 의문이 들 수 있습니다 
### 왜 굳이 Widget과 State를 나눌까?

사실 Flutter는 rebuild가 자주 일어나는데
<br>
Widget은 자주 새로 만들어도 가볍게 “구성”만 담고
<br>
State는 그 사이에서 계속 유지되어야 하는 값/리소스를 들고 있게 설계되었습니다
<br>
즉
- Widget: “이번 프레임에서 UI를 어떻게 그릴지” 설명
  
- State: “계속 유지할 데이터/컨트롤러/구독/타이머” 보관

한다고 보면 됩니다


## Stateful Widget 기본 형태
```dart
class CounterPage extends StatefulWidget {
  const CounterPage({super.key});

  @override
  State<CounterPage> createState() => _CounterPageState();
}

class _CounterPageState extends State<CounterPage> {
  int count = 0;

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text('$count'),
        ElevatedButton(
          onPressed: () => setState(() => count++),
          child: const Text('증가'),
        ),
      ],
    );
  }
}
```
- count는 State에 있음

- setState가 호출되면 build가 다시 호출

<br>

## setState()는 정확히 뭘 할까
setState(() { ... })는
<br>
State 내부 값을 변경하고

Flutter에게 “이 State가 관리하는 UI 다시 그려야 함”을 알려줍니다 (markNeedsBuild)

그리고 다음 프레임에서 build()를 다시 실행하게 만듭니다

setState는 “바로 build 실행”이 아니라<br>
rebuild 예약에 가깝죠 (프레임 타이밍에 맞춰 다시 그려줍니다)


# StatefulWidget 생명주기 (진짜 중요)

StatefulWidget의 생명주기는 사실 State 객체의 생명주기라고 보면 됩니다
물론 constructor(생성자)도 Stateful의 생명주기에 포함되지만 State생명주기와 구분 해야합니다

### StatefulWidget 쪽 생명주기 (constructor 포함)
```dart
class MyPage extends StatefulWidget {
  const MyPage({super.key}); // constructor

  @override
  State<MyPage> createState() => _MyPageState();
}
```
<b>이 단계에서 일어나는 일</b>

1. constructor 실행

2. widget 인스턴스 생성

3. createState() 호출

4. State 객체 생성

<br>

중요 포인트
- constructor는 Widget이 새로 만들어질 때마다 실행

- State는 아직 초기화되지 않음

- 여기엔 로직을 거의 넣지 않음

<br>

즉 constructor → createState() 까지는<br> “Widget 생명주기”


### State 생명주기
State쪽이 핵심이라고 볼 수 있죠
```
initState
→ didChangeDependencies
→ build
→ (setState → build 반복)
→ deactivate
→ dispose
```

그런데 이게 항상 전부 다 호출되지는 않습니다
상황에 따라 3가지 대표 시나리오로 나뉘죠

StatefulWidget 생명주기 3가지 시나리오

## 첫번째 사이클
처음 화면에 나타났다 → 사라지는 경우 (가장 기본)
### 예
- 앱 실행

- 페이지 push

- 페이지 pop

### 호출 순서 (constructor 포함)
```
[Widget]
constructor
createState

[State]
initState
didChangeDependencies
build
↓
(화면 사용)
↓
deactivate
dispose
```

### createState()
StatefulWidget이 트리에 들어갈 때 State를 만듭니다
<br>
보통 자동으로 override만 해두고 로직은 안 넣습니다

```dart
@override
State<CounterPage> createState() => _CounterPageState();

```

### initState()
State가 처음 생성된 직후 딱 한 번 호출됩니다

```dart
@override
void initState() {
  super.initState();
  // 초기화 로직
}
```
context 사용은 “대부분 가능”하지만
InheritedWidget에 의존하는 것(예: Theme.of(context), MediaQuery 등)은 보통 다음 단계에서 안전하답니다


### didChangeDependencies()
State가 InheritedWidget(Theme/MediaQuery/Provider 등)에 의존할 때 호출됩니다

initState 직후 1번은 무조건 호출되고

의존 대상이 바뀌면 또 호출됩니다
```dart
@override
void didChangeDependencies() {
  super.didChangeDependencies();
  // Theme/Locale/Provider 값 가져오기 적합
}
```

예:
- 다크모드 변경(Theme)

- 화면 회전(MediaQuery)

- Provider 값 변경


### build()
UI 구조를 반환합니다

실행되는 대표 상황:

- 처음 표시

- setState 호출

- 부모 rebuild

- dependencies 변화
```dart
@override
Widget build(BuildContext context) {
  return ...;
}
```

### deactivate()
State가 트리에서 제거되기 “직전”에 호출됩니다

다른 위치로 옮겨질 때(재삽입 가능)
Navigator 이동 등으로 잠깐 빠질 수도 있습니다

보통은 많이 안 쓰죵
```dart
@override
void deactivate() {
  super.deactivate();
}
```

### dispose()
State가 완전히 제거될 때 호출됩니다
<br>
여기서 리소스를 정리해야하죠

정리 대상:

- controller.dispose()

- stream subscription cancel

- timer cancel

- animation dispose
```dart
@override
void dispose() {
  // 정리 로직
  super.dispose();
}
```
dispose를 안 하면:
- 메모리 누수

- 이벤트 계속 들어와서 오류

- 앱 느려짐

이 발생합니다


<br>

## 두번째 사이클
상태만 바뀌는 경우 (setState)

<b>예</b>
- 버튼 클릭
- 카운트 증가

- 체크박스 토글

#### 호출 순서
```
(setState 호출)
→ build
```

#### 호출되지 않는 것
- constructor
- createState
- initState
- didChangeDependencies
- dispose

#### 이유
State 객체가 그대로 유지되기 때문에
UI만 다시 그려줍니다


## 세번째 사이클

부모가 새 Widget을 내려주는 경우 (didUpdateWidget)

<b>예</b>

```
Parent(
  child: MyPage(title: "A"),
);

// ↓ 부모 rebuild

Parent(
  child: MyPage(title: "B"),
);
```

#### 호출 순서
```
[Widget]
constructor (새 MyPage 인스턴스)

[State]
didUpdateWidget(oldWidget)
build
```

### 호출되지 않는 것
- initState
- dispose

### 이유

Widget만 교체되고 State는 그대로 재사용하기 때문입니다

### didUpdateWidget(oldWidget)
부모가 같은 타입의 위젯을 “새 인스턴스”로 넘겨주면
State는 유지되지만 Widget 설정이 바뀝니다 → 이때 호출

```dart
@override
void didUpdateWidget(covariant CounterPage oldWidget) {
  super.didUpdateWidget(oldWidget);
  // widget.xxx 값 변화에 반응
}
```

### 예:
- CounterPage(title: "A") → CounterPage(title: "B")로 바뀜

- State는 유지되지만 widget.title 값이 바뀌었으니 여기서 처리 가능



## Stateless vs Stateful

항목|Stateless|Stateful
|:-:|:-:|:-:|
상태 저장|X|O (State에 저장)
화면 갱신|부모 rebuild로만|setState로 가능
initState/dispose|X|O
사용처|고정 UI|값이 변하는 UI


