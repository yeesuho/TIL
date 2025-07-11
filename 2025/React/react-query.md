2025.04.23

React-query에 대해서 간단히 정리해 보겠습니다

# 리액트 쿼리를 왜 사용할까
React Query는 애플리케이션의 데이터를 관리하고 동기화하는데 사용 되는 라이브러리로 많은 개발자들에게 인기를 얻고 있는 상태관리 라이브러리 입니다

### 이유는 크게 다음과 같습니다
1) 간편한 데이터 관리
- 데이터 가져오기, 캐싱, 동기화 및 업데이트 처리를 간편하게 할 수있게 해줍니다
2) 실시간 업데이트 및 동기화
- 실시간 데이터 업데이트와 자동 동기화를 지원하여 서버와 클라이언트 데이터의 일관성을 유지합니다
3) 데이터 캐싱
- 데이터를 캐싱하여 불필요한 API 요청을 줄이고 애플리케이션의 성능을 향상 시킵니다
4) 서버 상태 관리
- 서버 상태 관리 (예를들면 로딩중, 에러, 성공 등의 상태)를 간편하게 처리할 수 있습니다
5) 간편한 설정
- React Query는 간단한 설정으로 사용할 수 있습니다

<br>

### 캐싱이란
Caching == Cache + ing<br>

Cache : 자주 필요한 데이터나 값의 복사본을 일시적으로 저장, 보관하기 위해 사용하는 곳<br>
Cacheing : cache를 사용하는 것