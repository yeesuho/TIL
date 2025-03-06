2025.03.06

## SQLD 공부 기록
### SELECT문 구조 및 실행순서

#### 작성 순서
1. SELECT: 최종적으로 뭘 표현하고 싶은가(대상 정의)
2. FROM: 데이터의 위치
3. WHERE: 조회 조건
4. GROUP BY: 그룹 연산을 할 때
5. HAVING: 그룹의 필터링 조건
6. ORDER BY: 정렬

<br>

#### 해석 순서
FROM ▶︎ WHERE ▶︎ GROUP BY ▶︎ HAVING ▶︎ SELECT ▶︎ ORDER BY

### SQL 문장 종류

|   |   |  |  |  |
|:------:|:----:|:----:|:----:|:----:|
| 데이터 조작어 <br> (DML)| DQL: SELECT  | INSERT  | UPDATE  | DELETE |
| 데이터 정의어 <br> (DDL) | CREATE  | ALTER  | DROP  | RENAME |
| 데이터 제어어 <br> (DCL) | GRANT  | REVOKE  |
| 트랜잭션 제어어 <br> (TCL) | COMMIT  | ROLLBACK  |