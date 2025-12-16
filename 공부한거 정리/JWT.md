2025.03.02
# JWT (Json Web Token) 알아보기

JWT란? 로그인 정보를 안전하게 주고받을 수 있는 토큰(Token) 방식의 인증 시스템

<br>

○ 쉽게 말하면<br>
✔로그인하면 서버가 **토큰(JWT)** 을 만들어서 사용자에게 줌 <br>
✔ 사용자는 이 토큰을 가지고 API 요청을 보냄 <br>
✔ 서버는 토큰을 확인하고 사용자를 인증함 <br>

세션 기반 로그인처럼 서버에서 세션을 저장하지 않아도 돼서, 빠르고 확장성이 좋음


## JWT가 왜 필요할까?
**기존 세션 기반 인증의 문제점**
<br>
로그인하면 서버가 세션을 저장하고, 사용자는 쿠키에 세션 ID를 저장함 <br>
하지만 사용자가 많아지면, 서버가 세션을 계속 관리해야 해서 부담이 커짐

<br>

**JWT 인증 방식**
<br>
JWT는 사용자 정보를 담은 토큰을 발급하고, <br>
사용자는 이 토큰을 API 요청 시 포함해서 보내기만 하면 인증 완료 <br>
✔ 서버가 사용자 정보를 따로 저장할 필요 없음 <br>
✔ 빠르고 확장성이 뛰어남 

<br>

## JWT 기반과 세션 기반 인증의 차이점
![image](/img/jwt%20기반%20인증,%20세션%20기반%20안증%20차이.png)


## JWT 구조

JWT는 3가지 정보를 포함하는 문자열(String) 형태의 토큰

예시 구조)
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InRlc3QiLCJpYXQiOjE2ODAxMjM0NTYsImV4cCI6MTY4MDEyNzA1Nn0.lc2pXpdYElYmZ0PoFXozZbLzz3eQFKnIr4nYB5D2bNA
```

JWT는 "점(.)"으로 구분된 3가지 부분으로 구성됨

1. Header (헤더): 알고리즘, 타입 정보
2. Payload (페이로드): 사용자 정보 (ID, 권한 등)
3. Signature (서명): 변조 방지를 위한 암호화

<br>

## JWT 로그인 과정
**1️) 로그인 요청**
<br>
사용자가 ID/PW 입력 후 로그인 요청
```
POST /login
{
  "username": "test",
  "password": "1234"
}
```

<br>

**2) 서버가 JWT 발급**
<br>
서버가 사용자를 확인하고 JWT 토큰을 생성해서 응답
```
(예시 토큰)
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6In..."
}
```
<br>

**3) API 요청 시 JWT 포함**
<br>
로그인 후, 사용자는 API 요청 시 JWT를 헤더에 담아서 전송
```
(http)
GET /profile
Authorization: Bearer <여기 JWT 토큰>
```
✔ GET /profile → 사용자의 프로필 정보를 가져오는 API
✔ Authorization: Bearer <JWT 토큰> → 인증을 위한 JWT 토큰을 헤더에 포함

💡 **"Bearer"**는 "이 토큰을 인증 수단으로 사용한다"는 의미

<br>

**4) 서버가 JWT 검증**
<br>
서버는 토큰을 확인하고 정상 사용자라면 데이터를 응답
```
{
  "message": "환영합니다, test!"
}
```

<br>

## 정리

JWT는 로그인 정보를 안전하게 주고받는 토큰 방식 인증 시스템<br>
서버가 인증 정보를 저장할 필요가 없어 확장성이 뛰어남<br>
하지만 보안 문제를 신경 써야 하며, Refresh Token을 함께 사용하면 안전함!