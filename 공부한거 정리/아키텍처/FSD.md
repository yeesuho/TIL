2025.05.14

# FSD(Feature-Sliced Design)

프론트엔드 코드베이스를 수직적(도메인) 관점으로 나누고, 각 영역의 책임과 경계를 명확히 하는 설계 방법론입니다

2025.05.15

### FSD의 기본 원칙
1) 수직적 분할(Vertical Slice)

- 기능(feature), 도메인(entity), 페이지(page) 단위로 코드를 묶어

- 각 레이어는 상위 레이어로부터만(또는 하위로만) 의존성을 가짐

2) 명확한 레이어 경계

 - 레이어 간 의존성 규칙:
```vbnet
app ← pages ← features ← entities ← shared
```
- 상위 레이어는 아래 레이어를 직접 참조할 수 있지만, 역방향(import) 금지


3) 재사용 가능한 shared 레이어
- 유틸리티, UI 컴포넌트, 타입 정의 등 모든 레이어에서 공통으로 쓰이는 것들만 모음


### 레이어별 역할
|레이어|역할
|:-:|:-:|
**app**|전역 설정·초기화(라우터, 테마, 전역 상태 프로바이더 등)
**pages**|URL별 화면 단위(Page 컴포넌트), 주로 라우팅에 연결
**features**|사용자 시나리오(로그인·댓글·검색 등) 단위 기능 묶음
**entities**|도메인 모델(유저, 게시물, 상품 등)의 데이터 구조·비즈니스 로직
**shared**|유틸리티 함수, 공통 UI 컴포넌트(Button, Modal), API 클라이언트 래퍼 등

### 디렉토리 구조
```plaintext
src/
├─ app/
│   ├─ router.tsx
│   └─ store.ts
│
├─ pages/
│   ├─ HomePage/
│   │   └─ HomePage.tsx
│   └─ ProfilePage/
│       └─ ProfilePage.tsx
│
├─ features/
│   ├─ auth/
│   │   ├─ model/        # redux slice, zustand store 등
│   │   ├─ ui/           # 로그인/회원가입 컴포넌트
│   │   └─ api/          # auth API 호출 함수
│   └─ comments/
│       ├─ model/
│       ├─ ui/
│       └─ api/
│
├─ entities/
│   ├─ user/
│   │   ├─ types.ts     # User 타입 정의
│   │   └─ service.ts   # user 관련 비즈니스 로직
│   └─ post/
│       ├─ types.ts
│       └─ service.ts
│
└─ shared/
    ├─ ui/               # Button.tsx, Modal.tsx 등
    ├─ utils/            # formatDate.ts, debounce.ts 등
    └─ config/           # axios instance, env 설정 등

```

###  레이어 간 의존성 예시
- pages/ProfilePage
```ts
import { useUser } from 'entities/user/service'    // 가능
import { ProfileCard } from 'features/profile/ui'  // 가능
// import { HomePage } from 'pages/HomePage'        // 사이클 방지를 위해 피해야 함

```
- features/auth
```ts
import { loginApi } from 'shared/api/authClient'   // shared 레이어만 참조

```
### 장점
- 유지보수성: 관심사별로 코드가 모여 있어 변경 범위가 좁아짐

- 확장성: 새로운 기능(feature)을 추가할 때 폴더만 생성 -> 다른 레이어에 영향 최소화

- 협업 효율: 팀 간 역할 분담(백엔드, UI, 도메인 로직)이 분산되어 충돌 감소

- 테스트 용이: 레이어별 경계가 명확해 단위 테스트 범위 설정이 쉬움

