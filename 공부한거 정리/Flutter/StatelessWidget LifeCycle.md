2025.12.27

Life Cycle이 뭔지 모르는 분들은 Life Cycle 내용을 먼저 보고 오시는걸 추천드립니다

## Stateless Widget이란?
>상태(state)를 가지지 않는 위젯

### StatelessWidget은 immutable(불변)한 Widget 객체
- 내부에 변경 가능한 상태를 저장하지 않음

- 한 번 생성되면 자기 자신을 변경하지 않음

- UI는 오직 생성자 인자 + BuildContext에 의해서만 결정됨


StatelessWidget = 상태(변하는 값)를 안 들고 있는 화면 조각<br>
즉 자기 혼자서는 절대 안 바뀌고 바뀌려면 밖(부모)에서 값이 새로 들어와야 합니다

여기서 state(상태)는 이런 것:
- 좋아요 눌렀는지 (true/false)

- 카운트 값 (0, 1, 2…)

- 로딩 중인지 (loading)

- 체크박스 체크 여부

<hr>
이런 변하는 값을 위젯이 직접 들고 있으면 → Stateful<br>
그런 값이 없으면 → Stateless

<br>



### Stateless인데 화면이 바뀌던데요??
StatelessWidget 자체는 바뀌지 않습니다

#### 화면이 바뀌는 이유는:

1.  부모 위젯의 상태 변경

2. 부모 build 재실행

3. 새 StatelessWidget 인스턴스 생성

4. 이전 인스턴스는 폐기

5. 새 인스턴스의 build 실행

즉: StatelessWidget은 수정되는 것이 아니라 교체된다 라고 보면 됩니다



## 코드로 보자면
```dart
class MyText extends StatelessWidget {
  final String title;

  const MyText({super.key, required this.title});

  @override
  Widget build(BuildContext context) {
    return Text(title);
  }
}
```
title 값이 바뀌려면
→ 부모가 새로운 MyText를 다시 만들어줘야 함

<br>

## Stateless의 생명주기
```
(1) 생성자 실행 → (2) build 실행 → (3) 필요 없으면 버림
```

### 단계별 상세 설명
위에 코드를 예시로 설명해보겠습니다
### ① 생성자 (constructor)
```dart
const MyText({super.key, required this.title});
```
- 위젯 객체가 메모리에 생성

- 여기서는 로직 X

- 값 저장만 함

### ② build()
```dart
@override
Widget build(BuildContext context) {
  return Text(title);
}
```
build()는 이럴 때 호출이 됩니다

상황|호출 여부
|:-:|:-:|
처음 화면에 나타날 때|O
부모 위젯이 rebuild 될 때|O
MediaQuery 변경 (회전 등)|O
Theme 변경|O
Navigator push/pop|O

#### build()는 여러 번 호출됩니다
그래서 build 안에는 가벼운 UI 코드만 있어야 하죠
위험한 코드(API 호출)
```dart
build() {
  fetchData(); // ❌
}
```

### ③ 제거 (destroy)
StatelessWidget은<br>
dispose()가 없습니다<br>(dispose 내용은 Stateful Widget을 확인해주세요)

왜냐하면?
- 유지할 상태가 없기 때문

- Flutter가 그냥 메모리에서 버려버림 (GC)

```
[ 생성자 ]
     ↓
[ build() ]
     ↓
( 필요 없으면 제거 )
```




<br>

## “Rebuild” ≠ “새로 생성”
이것도 중요한 개념인데
개념|의미
|:-:|:-:|
rebuild|build()만 다시 호출
recreate|생성자부터 다시 실행

```dart
MyText(title:"A")
```
부모위젯이 이렇게 바꾸면
```dart
MyText(title:"B")
```
- 이전 위젯 제거
- 새 위젯 생성
- build() 실행



## 그럼 언제 Stateless를 써야 할까요

- 텍스트 표시

- 아이콘

- 버튼 UI

- 기타 상태가 없는 위젯

기본 원칙: “상태가 없으면 Stateless부터”