2025.05.16

ArrayList는 가장 많이 쓰이는 컬렉션 클래스 중 하나입니다<br>
쉽게 말하자면 배열처럼 여러 개의 데이터를 담는 자료구조인데 배열보다 훨씬 유연하고 편리한 기능들을 제공합니다


## ArrayList란?
- ``java.util`` 패키지에 있는 가변 크기의 배열 클래스

- 크기를 자동으로 늘릴 수 있는 배열

- 순서가 유지되고, 중복을 허용

- List 인터페이스를 구현하고 있음

### 사용 예)
```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();

        list.add("사과");
        list.add("바나나");
        list.add("똥");

        System.out.println(list.get(0)); // 사과
        System.out.println(list.size()); // 3
    }
}
```


### 주요 메서드 정리




|메서드|설명
|:-:|:-:|
``add(E e)``|요소 추가
``add(int index, E)``|특정 위치에 요소 추가
``get(int index)``|요소 가져오기
``set(int index, E)``|요소 수정
``remove(int index)``|요소 삭제
``clear()``|모든 요소 제거
``size()``|요소 개수 반환
``isEmpty()``|비었는지 확인
``contains(Object o)``|해당 요소 포함 여부 확인

### ArrayList의 특징
- null 값도 넣을 수 있음

- 내부적으로는 배열로 구현되어 있음

- 동기화되지 않음 (=> 멀티스레드에서는 Vector 또는 Collections.synchronizedList() 사용한다고 하네요)

    - 여기서 동기화 되지 않는 다는 말은 <br>여러 개의 스레드가 동시에 같은 데이터를 건드릴 때 문제가 생기지 않도록 보호하는 것<br>
    예를 들어서:
        - 두 사람이 동시에 같은 문서 파일을 수정하면 내용이 꼬일 수 있죠

        - 컴퓨터에서는 그런 상황을 막기 위해 하는 걸 동기화라고 합니다

    - ArrayList는 기본적으로 여러 스레드에서 동시에 접근하면 문제가 생길 수 있어서 <br>
    멀티스레드 환경(= 동시에 여러 작업이 돌아가는 환경)에서는 주의가 필요합니다

<br>

그럼 여기서 생기는 궁금증 2차원 배열 처럼 2차원 ArrayList도 가능할까요??<br>
네 가능합니다

### 2차원 ArrayList 기본 구조
```java
ArrayList<ArrayList<Integer>> matrix = new ArrayList<>();
```
``matrix``는 2차원 리스트

``matrix.get(0).get(1)`` 이런 식으로 접근 가능


예시) 2x3 리스트 만들기
```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<ArrayList<Integer>> matrix = new ArrayList<>();

        // 2개의 행 만들기
        for (int i = 0; i < 2; i++) {
            ArrayList<Integer> row = new ArrayList<>();
            for (int j = 0; j < 3; j++) {
                row.add(i * 10 + j); // 예: 0, 1, 2 / 10, 11, 12
            }
            matrix.add(row); // 행을 matrix에 추가
        }

        // 출력하기
        for (int i = 0; i < matrix.size(); i++) {
            for (int j = 0; j < matrix.get(i).size(); j++) {
                System.out.print(matrix.get(i).get(j) + "\t");
            }
            System.out.println();
        }
    }
}

```

### 결과
```java
0	1	2	
10	11	12
```
``ArrayList<ArrayList<T>>`` 형태로 만들면 자바에서도 2차원 배열처럼 쓸 수 있고 일반 배열(``int[][]``)보다 조금 느릴 수 있지만 유연성이 높습니다