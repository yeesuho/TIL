2025.12.27

## MediaQuery.of(context)
mdOf라고 입력해도 자동 완성이 돼서 mdOf라고 부르겠습니닷

```dart
final size = MediaQuery.of(context).size;
```
보통 이런식으로 사용되고
- 현재 디바이스 화면의 실제 크기
- 상태바, 네비게이션바 등을 제외한 논리적 화면 크기
를 뜻한답니다

그냥 쉽게 말하면 현재 사용하는 기기의 가로 세로 크기를 구할 수 있는겁니다

### 예시
```dart
Container(
  width: MediaQuery.of(context).size.width,
  height: MediaQuery.of(context).size.height,
)

```
이렇게 하면 컨테어너가 화면 전체 크기를 차지합니다

### 특징
- 기기 기준
- 가로/세로 회전 시 값 변경됨
- 부모 위젯과 상관없이 스크린 기준


## double.infinity
- 부모가 허용하는 최대 크기까지 늘어남
- “무한”이 아니라 제약(constraints) 내 최대값


### 예시
``` dart 
Container(
  width: double.infinity,
  height: 50,
)
```
부모 위젯의 가로폭을 꽉 채웁니다

### 특징
- 부모 위젯 기준
- 부모가 크기를 제한하면 그 안 까지만 확장
- 부모가 제약이 없으면 에러발생 가능

<br>


# 차이 표



|구분|MediaQuery.of|double.infinity|
|:-:|:-:|:-:|
|기준|화면|부모위젯|
|의미| 실제 디바이스 크기| 허용된 최대 크기|
|반응형| 기기 회전/크기 변화| 부모 레이아웃 변화|
|에러 위험| 거의 없음| 제약 없으면 에러|
|용도|전체 화면 기준 UI|부모 꽉 채우기|
