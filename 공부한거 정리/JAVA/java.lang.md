2025.05.02


### java.lang 패키지는 뭐하는 곳일까
java.lang은 자바 프로그램을 작성할 때 꼭 필요한 기본 클래스들을 모아놓은 패키지

### 대표적인 클래스들
| 클래스                                        | 설명                            |
| ------------------------------------------ | ----------------------------- |
| `Object`                                   | 모든 클래스의 최상위 부모 클래스            |
| `String`                                   | 문자열을 다루는 클래스                  |
| `StringBuilder`, `StringBuffer`            | 변경 가능한 문자열 처리 클래스             |
| `Math`                                     | 수학 계산용 유틸리티 클래스               |
| `Integer`, `Double`, `Boolean` 등           | 기본 타입을 객체로 다루는 래퍼 클래스         |
| `System`                                   | 표준 입출력, 환경 변수, 시간 등 시스템 관련 기능 |
| `Thread`                                   | 쓰레드(동시 실행) 관련 기능              |
| `Exception`, `RuntimeException`, `Error` 등 | 예외 처리 관련 클래스                  |

<br>

### 예시)
```java
public class Main {
    public static void main(String[] args) {
        // String
        String s = "Hello";
        System.out.println(s.length());  // 문자열 길이

        // Math
        System.out.println(Math.sqrt(16));  // 제곱근

        // Integer
        int num = Integer.parseInt("123");  // 문자열 → 정수 변환

        // System
        System.out.println(System.currentTimeMillis());  // 현재 시간(ms)

        // Object
        Object obj = new String("Hi");
        System.out.println(obj.toString());  // 업캐스팅된 String
    }
}
```

### 요약
요약하자면 java.lang은 기본 클래스들의 모음집이고<br> 자바 프로그램에서 항상 사용하는 기능들이 들어있음

별도의 import 없이 자동으로 사용 가능

