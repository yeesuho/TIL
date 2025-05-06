2025.05.07

1.리액트(React)에서 AJAX는 서버와 비동기적으로 데이터를 주고받을 때 사용됨

2.페이지를 새로 고치지 않고도 서버에서 데이터를 가져오거나 보낼 수 있게 해줌

보통 다음 두 가지 방법으로 AJAX 요청을 보낼 수 있음

### ```fetch``` 사용 (브라우저 내장 API)
```jsx
useEffect(() => {
  fetch('https://api.example.com/data') // 서버 주소
    .then((response) => response.json()) // 응답을 JSON으로 변환
    .then((data) => {
      console.log(data); // 가져온 데이터 사용
    })
    .catch((error) => {
      console.error('Error:', error); // 에러 처리
    });
}, []);
```
- useEffect: 컴포넌트가 처음 렌더링될 때 실행됨 (마운트 시점)

- ``fetch``: 서버에 비동기 요청을 보냄

- ``.then()``: 응답을 처리

- ``.catch()``: 에러 처리


### axios 사용 (외부 라이브러리)
먼저 설치
```bash
npm install axios
```

사용 예)
```jsx
import axios from 'axios';
import { useEffect } from 'react';

function MyComponent() {
  useEffect(() => {
    axios.get('https://api.example.com/data')
      .then((response) => {
        console.log(response.data); // 응답 데이터
      })
      .catch((error) => {
        console.error('Error:', error); // 에러 처리
      });
  }, []);

  return <div>데이터 로딩 중...</div>;
}
```

- axios.get: GET 요청

- axios.post: POST 요청 등 다양한 메서드 제공


### AJAX는 언제 쓸까
- 서버에서 데이터 목록 불러오기

- 폼 데이터를 서버로 전송하기

- 로그인/회원가입 처리

- CRUD(생성, 읽기, 수정, 삭제) 작업

