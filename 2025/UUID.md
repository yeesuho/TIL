2025.05.21

UUID는 Universally Unique Identifier의 약자입니다<br>
전 세계적으로 고유한 식별자를 만들기 위해 사용됩니다<br>
주로 데이터베이스나 분산 시스템에서 중복되지 않는 ID가 필요할 때 많이 사용합니다

## UUID의 특징
- 128비트(16바이트) 크기의 값

- 사람이 보기 쉽도록 일반적으로는 32자리의 16진수를 8-4-4-4-12 형식으로 표현합니다

예시)
```
f47ac10b-58cc-4372-a567-0e02b2c3d479
```

## UUID의 버전
UUID는 여러 버전이 있는데
<br>대표적인 것만 정리해보겠습니다
|버전|설명
|:-:|:-:|
v1|현재 시간 + MAC 주소 기반 (중복 가능성이 낮지만, 보안 취약)
v3|이름 기반 + MD5 해시
v4|랜덤 값 기반 (가장 흔히 사용됨)
v5|이름 기반 + SHA-1 해시

=> 보통은 ``v4(UUID.randomUUID())``를 가장 많이 사용한다고 합니다<br> 간단하고 충돌 가능성도 거의 없기 때문이라고 하네요


## 언제 사용하냐면
- 사용자 ID, 세션 ID

- 데이터베이스 기본키(특히 분산 시스템에서)

- 파일 이름 등 중복되지 않아야 하는 모든 상황

### 예시(Java)
```java
import java.util.UUID;

public class Example {
    public static void main(String[] args) {
        UUID uuid = UUID.randomUUID();
        System.out.println("UUID: " + uuid.toString());
    }
}
```
출력 예시:
```makefile
UUID: 3e1fc424-48f7-4f8b-bc97-77a4a5e3c95e
```

### JavaScript에서 UUID 생성 예시
JavaScript에는 기본적으로 UUID 생성 기능이 없지만 라이브러리를 사용하거나 브라우저 내장 API를 사용할 수 있습니다
### 방법 1: crypto.randomUUID() (최신 브라우저 지원)
```js
const uuid = crypto.randomUUID();
console.log("UUID:", uuid);
```
#### 예시 출력:
``UUID: e1d9b4c4-2f5c-42e7-a4cc-6bcd60f9d142``

### 방법 2: uuid 라이브러리 사용 (Node.js, 프로젝트용)
설치:
```bash
npm install uuid
```
사용:
```js
import { v4 as uuidv4 } from 'uuid';

const uuid = uuidv4();
console.log("UUID:", uuid);
```
예시 출력:
``UUID: 8c06ed8b-2074-46cb-8b3b-7d8d5e53d8d7``

### Swift에서 UUID 생성 예시
Swift에서는 UUID 구조체가 기본 제공돼서 간단합니다
```swift
import Foundation

let uuid = UUID()
print("UUID: \(uuid.uuidString)")
```
예시 출력:
``UUID: 5E3B821F-72CD-4A2B-86A6-0E84D9F6D36F``

``UUID()``는 무작위로 생성된 v4 UUID를 반환함

``uuid.uuidString``으로 문자열 형태로 변환 가능