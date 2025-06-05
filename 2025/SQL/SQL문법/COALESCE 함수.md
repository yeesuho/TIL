2025.06.06

COALESCE 함수는 SQL에서 NULL이 아닌 첫 번째 값을 반환하는 함수입니다

여러 개의 값 중에서 가장 먼저 NULL이 아닌 값을 찾아서 반환해주는거죠

### 기본 문법

```sql
COALESCE(value1, value2, value3, ..., valueN)
```
value1부터 valueN까지 순서대로 검사해서
- 가장 먼저 NULL이 아닌 값을 반환

- 전부 NULL이면 NULL을 반환


## 예시
```sql
SELECT COALESCE(NULL, NULL, 'Hello', 'World');
```
결과: `'Hello'`
- NULL, NULL은 무시되고 'Hello'가 반환

### 컬럼에 사용
```sql
SELECT name, COALESCE(nickname, '없음') AS nick_display
FROM users;
```
- nickname이 NULL이면 "없음"으로 표시

<br>

### 여러 컬럼 비교
```sql
SELECT COALESCE(phone_home, phone_work, phone_mobile, '연락처 없음') AS contact
FROM employees;
```
집 전화 -> 회사 전화 -> 핸드폰 순으로 확인하고
- 전부 NULL이면 '연락처 없음' 출력


