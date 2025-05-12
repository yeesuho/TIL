2025.05.12

socket.io와 **웹소켓(WebSocket)**은 비슷한 역할을 하지만 엄연히 다르다고 합니다 개념 정리를 해보겠습니다

### 표로 비교하기

|항목|WebSocket|Socket.IO|
|:-:|:-:|:-:|
정의|브라우저와 서버 간의 양방향 통신 프로토콜|WebSocket 기반의 라이브러리
표준 여부|W3C, IETF에서 정의된 표준 프로토콜|비표준 (라이브러리)
기반 기술|WebSocket 프로토콜 (ws://, wss://)|WebSocket + HTTP long polling 등 다양한 방식
자동 재접속|없음 (직접 구현해야 함)|자동 재접속 지원
방(Rooms)|직접 구현 필요|내장 기능으로 지원
이벤트 시스템|수동 구현 (onmessage 등)|socket.on('event')으로 간편
브라우저 지원|대부분의 최신 브라우저|브라우저+Node.js 모두 지원
설정 난이도|낮음 (간단)|조금 높음 (서버-클라이언트 모두 설정 필요)


### WebSocket이란?
- 기본 기술: HTML5 표준

- 주 목적: 빠르고 가벼운 실시간 양방향 통신

- 클라이언트와 서버가 연결을 유지하며 데이터를 주고받음
```js
const ws = new WebSocket('ws://localhost:3000');
ws.onmessage = (event) => {
  console.log('메시지 받음:', event.data);
};
ws.send('Hello server!');
```

### Socket.IO란?
- WebSocket 위에 구축된 라이브러리

- WebSocket이 안 되는 환경에서는 Long Polling으로 대체

- 이벤트 기반 구조로 코드가 깔끔해짐

- 방(room), 네임스페이스, 자동 재연결, 연결 상태 확인 기능 등 많은 기능 제공
```js
const socket = io('http://localhost:3000');
socket.on('chat', (msg) => {
  console.log('채팅 메시지:', msg);
});
socket.emit('chat', '안녕 서버!');
```

결론적으로 socket.io가 websocket을 기반으로 다양한 기능을 얹은 라이브러리인 것 같습니다

원하는 것이 단순한 실시간 통신이면 WebSocket이 좋고<br>
실시간 채팅, 게임, 협업 등 복잡한 앱이면 socket.io가 더 편리하다고 합니다