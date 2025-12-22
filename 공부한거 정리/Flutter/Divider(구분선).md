2025.12.22

# Flutter - Divider
Divider는 HTML에 `<hr>` 같은 녀석입니다<br>
그럼 바로 Flutter에서 구분선을 어떻게 구현하는지 알아보겠습니다

## 1. 기본적인 가로 구분선
### 구현
```dart
Divider(thickness: 1, height: 1, color: color)
```
<br>

### Divider.dart 생성자
```dart
const Divider({
    Key? key,
    this.height,
    this.thickness,
    this.indent,
    this.endIndent,
    this.color,
})
```

## 2. 세로 구분선
### 구현
```dart
VerticalDivider(thickness: 1, width: 1, color: color)
```
### VerticalDivider.dart 생성자
```dart
const VerticalDivider({
    Key? key,
    this.width,
    this.thickness,
    this.indent,
    this.endIndent,
    this.color,
})
```


여기서 
height와 width는 요소 사이에 있는 Divider에 
전체 높이와 넓이를 의미 합니다 
실제 선(thickness)을 가운데에 놓고 남는 공간을 위/아래로 반반 나눠서 여백처럼 씁니다 그래서 굳이 `SizedBox()`를 쓸필요가 없죵

<br>

thickness는 선의 굵기를 뜻합니다<br>
`thickness: 1` = 1lp(logical pixel)짜리 선<br>
근데 헷갈릴 수 있는게 thickness가 늘어난다고 해서 width나 height가 늘어나진 않습니닷<br>
안헷갈리셨다고요?? 저는 헷갈렸어요..

<br>

indent와 endIndent는 선의 좌우 시작/끝 여백(들여쓰기) 입니다<br>
`indent:`왼쪽에서 얼마난 띄우고 선을 시작할지<br>
`endIndent:`오른쪽에서 얼마나 띄우고 선을 끝낼지

<br>

그리고 horizon과 vertical 둘의 차이는 width냐 height냐 차이입니다<br>
horizon(수평) 가로는 height<br>
vertical(수직) 세로는 width