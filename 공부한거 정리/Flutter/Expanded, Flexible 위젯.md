2025.12.16

## Expanded 와 Flexible을 알아봅시다

Row 혹은 Column 등등 Children으로 박스(Container 혹은 SizedBox 등등)를 넣을 경우 width나 height으로 위젯의 크기(lp)를 지정해줄 수 있지만 절대적인 값이 아닌 비율(%)로 설정하고자 할 때가 있죠

<br>

# Expanded
예시를 위해 다음과 같이 body에 Row를 지정하고 children 하위에 박스를 2개 정도 배치해줍니다
```dart
@override
  Widget build(BuildContext context) {
    return MaterialApp(
        home: Scaffold(
            appBar: AppBar(),
            body: Row(
              children: [
                Container(),
                Container(),
              ],
            )));
  }
  
```

Container의 괄호 안에 width 혹은 height로 위젯의 크기를 정적으로 지정할수도 있지만 Expended를 사용해봅시다

각각의 박스에 색을 입히고 출력 결과를 확인해보죠
```dart
@override
  Widget build(BuildContext context) {
    return MaterialApp(
        home: Scaffold(
            appBar: AppBar(),
            body: Column(
              children: [
                Expanded(
                  // Container를 Expanded로 감싸준 빨간색 박스
                  child: Container(
                    color: Colors.red,
                  ),
                ),
                Expanded(
                  // Container를 Expanded로 감싸준 파란색 박스
                  child: Container(
                    color: Colors.blue,
                  ),
                ),
              ],
            )));
  }
```
Expanded는 부모의 요소를 자식의 요소로 꽉채우고 싶을 경우에 사용합니다 

Expanded로 감싼 요소는 flex:1 의 배수를 가진 Flexible이랑 똑같기 때문에 빨간색 박스와 파란색 박스가 각각 화면을 절반씩 차지하고 있는 것을 볼수 있죠

![img](/img/Expanded.png)

Expanded와 flex: 값을 적용한 Flexible 박스가 동시에 존재할 경우, flex:에 지정한 배수만큼의 비율을 적용 후 나머지 공간을 Expanded가 차지하게 됩니다

![img](/img/Expanded와%20flex-%20값을%20적용한%20Flexible%20박스가%20동시에%20존재할%20경우.png)

<br>

# Flexible
이번에는 Flexible을 사용해보죠

먼저 Container를 다음과 같이 Flexible()로 감싸줍니다

``` dart
@override
  Widget build(BuildContext context) {
    return MaterialApp(
        home: Scaffold(
            appBar: AppBar(),
            body: Row(
              children: [
                Flexible( // Container를 Flexible로 감싸준 빨간색 박스
                    child: Container(
                  color: Colors.red,
                )),
                Flexible( // Container를 Flexible로 감싸준 파란색 박스
                    child: Container(
                  color: Colors.blue,
                )),
              ],
            )));
  }
```
![img](/img/flexible%20flex값%20적용전.png)
-`flex:`값 적용 전-



이후 Container() 옆에 다음과 같이 flex 파라미터를 추가하여 원하는 배수를 적어줘봅시다

전체를 10으로 볼 때 빨간색 박스에는 2, 파란색 박스에는 8의 비율을 지정해주면 red와 blue의 화면 비율은 2:8이 됩니다

```dart
@override
  Widget build(BuildContext context) {
    return MaterialApp(
        home: Scaffold(
            appBar: AppBar(),
            body: Row(
              children: [
                Flexible( // Container를 Flexible로 감싸줌, 빨간색 박스
                  child: Container(
                    color: Colors.red,
                  ),
                  flex: 2,  // flex: 배수
                ),
                Flexible( // Container를 Flexible로 감싸줌, 파란색 박스
                  child: Container(
                    color: Colors.blue,
                  ),
                  flex: 8,  // flex: 배수
                ),
              ],
            )));
  }
```
- `flex:` 값 적용 후 Row
![img](/img/flex%20값%20적용%20후%20Row.png)
- `flex:` 값 적용 후 Column
![img](/img/flex값%20적용%20후%20Column.png)

Row를 Column으로 바꾸더라도 가로 세로의 차이만 존재할 뿐 비율에 따라 배치되는 것을 볼 수 있습니다

<br>



### Flexible을 한 번 사용해봅시다



## Flexible과 Expanded 차이
||Flexible|Expanded|
|:-:|:-:|:-:|
|child가 부모보다 클 경우|부모 크기에 맞게 최대로 확장됨|부모 크기에 맞게 최대로 확장됨|
|child가 부모보다 작을 경우	|크기 변화 없음|부모 크기에 맞게 최대로 확장됨|



### 글자가 아닌 도형 같은걸 배치할땐 Expanded를 더 많이 쓴다고 하네요