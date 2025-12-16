2025.06.02

DECODE는 Oracle SQL에서 자주 사용되는 조건문 함수로, IF-THEN-ELSE나 CASE 구문처럼 값에 따라 결과를 다르게 반환할 때 사용합니다

그럼 바로 알아보죠

### 기본  문법
```sql
DECODE(표현식, 조건1, 결과1, 조건2, 결과2, ..., [기본값])
```
### 작동 방식
1. 표현식과 조건1, 조건2, ... 를 순차적으로 비교

2. 일치하면 해당 결과를 반환

3. 일치하는 조건이 없으면 기본값을 반환 (생략하면 NULL)


### 예제
#### 예시 1: 숫자 → 문자열로 변환
```sql
SELECT 
  empno,
  ename,
  deptno,
  DECODE(deptno, 
         10, '총무부', 
         20, '인사부', 
         30, '영업부', 
         '기타') AS 부서명
FROM emp;
```
``deptno``가 10이면 '총무부', 20이면 '인사부', 30이면 '영업부', 나머지는 '기타'로 표시

<br>

#### 예시 2: 성별 코드 → 성별명 변환
```sql
SELECT 
  name,
  gender,
  DECODE(gender, 
         'M', '남자', 
         'F', '여자', 
         '기타') AS 성별
FROM students;
```


### CASE와 비교
```sql
-- DECODE
DECODE(score, 90, 'A', 80, 'B', 70, 'C', 'F')

-- CASE
CASE 
  WHEN score = 90 THEN 'A'
  WHEN score = 80 THEN 'B'
  WHEN score = 70 THEN 'C'
  ELSE 'F'
END

```
``DECODE:`` 단순한 **동등 비교(=)**만 가능

``CASE:`` 범위 조건, 복잡한 조건문도 가능



### 그럼 DECODE를 주로 사용하는 경우는 언제일까
1. 단순한 값 매핑 (코드 → 명칭)<br>
예를 들어, 숫자 코드나 문자열 코드가 특정 의미를 가질 때:
```sql
SELECT 
  DECODE(job_code, 
         'A1', '관리자', 
         'B2', '사원', 
         'C3', '임원', 
         '기타') AS 직책
FROM employees;
```
>코드 값을 사람이 읽을 수 있는 값으로 바꾸고 싶을 때 많이 사용됩니더

<br>

2. 빠르게 IF처럼 쓰고 싶을 때 (간단한 조건 1~2개)
```sql
SELECT 
  empno,
  ename,
  DECODE(comm, NULL, '보너스 없음', '보너스 있음') AS 보너스상태
FROM emp;
```
>NULL 여부 판단도 간단하게 할 수 있어서 빠르게 쓸 수 있죠

3. 그룹핑이나 집계 조건 만들 때
```sql
SELECT 
  DECODE(deptno, 10, '총무부', 20, '인사부', '기타') AS 부서,
  COUNT(*) AS 인원수
FROM emp
GROUP BY DECODE(deptno, 10, '총무부', 20, '인사부', '기타');
```
>GROUP BY나 ORDER BY에도 간단하게 매핑해서 쓰기 좋아요


## CASE를 쓰는게 나은 케이스
- 비교 조건이 = (같다) 외에 <, >, BETWEEN, IS NULL 등인 경우

- 조건이 많거나 복잡한 경우

- 다른 SQL (MySQL, PostgreSQL 등)에서는 DECODE가 지원되지 않아서 CASE가 표준입니다

