2026.02.11

# List.generate란?
Dart에서 제공하는 기능으로<br>
``List.generate``는 원하는 길이의 리스트를 만들면서<br>
각 인덱스마다 값을 계산해서 채우는 함수입니다

특정 개수의 리스트를 빠르게 생성할때 사용됩니다
```dart
List<T> List.generate(
  int length,
  T Function(int index) generator,
  {bool growable = false}
)
```
- length: 생성할 리스트의 길이
- generator: 각 인덱스에 대한 값을 생성하는 함수
- growable: 기본값은 false이며 true로 설정하면 리스트를 동적으로 확장 가능하게 만듭니다



### 기본 형태
```
List.generate(length, (index) => 값);
```
- length: 리스트 길이 (몇개 만들지)
- (index) => 값: 0 부터 시작하는 index를 받아서 그 인덱스에 들어갈 값을 만들어 반환

저는 generate 문법을 보면서 Swift에 ``stride``랑 비슷하고 느꼈습니다 문법은 다르긴 한데 사용하는 이유는 비슷한거 같아요

#### 결과
```dart
final list = List.generate(5, (i) => i);
print(list); // [0, 1, 2, 3, 4]
```


## 자주 쓰는 패턴

### 1) 1~n 만들기
```dart
final nums = List.generate(5, (i) => i + 1);
print(nums); // [1, 2, 3, 4, 5]
```


### 2) 같은 값으로 채우기
```dart
final zeros = List.generate(4, (_) => 0);
print(zeros); // [0, 0, 0, 0]
```

`_`는 `안 쓸 변수`라는 뜻 (index 안 쓸 때 많이 씀) -  Swift로 알고리즘 풀때 많이 써서 익숙하네요

### 3) 계산 결과로 채우기
```dart
final squares = List.generate(6, (i) => i * i);
print(squares); // [0, 1, 4, 9, 16, 25]
```

### 4) Widget 리스트 만들기 (Flutter에서 많이 씀)
```dart
final items = List.generate(
  3,
  (i) => Text("Item $i"),
);
```

## 번외: 2차원 리스트 생성
```dart
void main() {
  List<List<int>> matrix = List.generate(3, (i) => List.generate(3, (j) => i + j));
  print(matrix);
}
```
2차원 리스트도 이런식으로 generate 안에 generate를 쓰는 방식으로 사용할 수 있습니다