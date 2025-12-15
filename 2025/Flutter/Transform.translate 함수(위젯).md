2025.12.15

기능대회 아자아자

## 1. Transform.translate란?
주어진 Widget을 지정된 x 및 y 좌표로 이동시키는데 사용됩니다<br>
이 함수는 Transform 위젯의 일부로 사용되며 이를 위해 Widge을 변환하고 조작할 수 있습니다

<br>

## 2. 기본 구조
```dart
Transform.translate(
    offset: Offset(dx, dy),
    child: YourWidget(),
)
```

<br>

## 3. 매개변수
|매개변수|설명|
|:-:|:-:|
|offset|Offset 객체를 통해 이동할 거리를 지정 Offset은 x 및 y 좌표를 <br>나타내는데 사용 되며,<br> Offset(dx, dy) 형태로 생성.<br> dx: x축으로 이동 거리<br> dy: y 축으로의 이동 거리|
|child|이동시킬 대상이 되는 Widget을 지정.<br>Transform.translate는 이 Widget을<br> 주어진 offset만큼 이동시킨 새로운 Widget을 생성.|

<br>

## 사용 예시
(Transform.translate를 사용하여 텍스트를 x축으로 50, y축으로 100만큼 이동)
```dart
Transfom.translate(
    offset: Offset(50.0, 100.0),
    child: Text('Flutter'),
)
```
