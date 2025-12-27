2025.12.27

먼저 Stateless Widge과 Statefull Widget의 생명주기(Life Cycle)을 알아보기 전에 Life Cycle이 뭔지 개념을 알고 넘어가보겠습니다

## Life Cycle(생명주기)란?
객체또는 화면, 위젯이 생성되어 -> 사용되고 -> 사라질 때까지의 전 과정을 뜻하고
```
태어남 → 일함 → 죽음
```
이 흐름을 Life Cycle(생명주기)라고 부릅니닷

### 그럼 왜 Life Cycle 개념을 알아야할까?
뭐 Life Cycle 개념을 모른다고 죽는건 아니지만 Flutter를 기준으로 아래와 같은 문제가 생길 수 있습니다

- 언제 코드가 실행되는지 모름
- 메모리 누수 발생
- 화면이 이상하게 다시 그려짐
- API를 여러 번 호출함

- dispose 안 해서 앱 느려짐

"이 코드는 언제 실행돼야 하지?" 라는 질문에 답이 Life Cycle 이라고 볼 수 있습니다

### 아직 Life Cycle에 대해 잘 모르시겠다고요??
그럼 현실 세계로 비유해보겠습니다

#### 사람의 Life Cycle
```
출생 → 성장 → 활동 → 노화 → 사망
```

#### Flutter 위젯의 Life Cycle
```
생성 → 화면에 그림 → 필요 없어짐
```

#### 객체의 Life Cycle
```
메모리 할당 → 사용 → 메모리 해제
```

<br>

## Life Cycle이 적용되는 대상들
### 사실 Life Cycle은 거의 모든 것에 있답니다

대상|예시
|:-:|:-:|
객체(Object)|class 인스턴스
위젯(Widget)|Stateless / Stateful
화면(Screen)|페이지
앱(App)|실행 → 백그라운드 → 종료
스트림|구독 → 수신 → 해제



### “언제 쓰는 개념이냐”를 예로 보면

#### API 호출은 언제 → initState

#### 화면 다시 그릴 때는 → build

#### 타이머 종료 → dispose

이게 전부 Life Cycle 기준 판단