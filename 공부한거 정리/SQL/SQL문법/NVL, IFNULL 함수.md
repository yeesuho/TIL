2025.06.07

IFNULL은 MySQL 전용 함수이고
<br>
Oracle에서는 IFNULL이 없고 대신 NVL을 사용합니다


## IFNULL (MySQL 전용)

### 문법
```sql
IFNULL(값1, 값2)
```
- 값1 이 NULL이면 => 값2 반환

- 값1이 NULL이 아니면 => 값1 그대로 반환


### 예시
```sql
SELECT IFNULL(NULL, '기본값'); 
-- 결과: '기본값'

SELECT IFNULL('안녕', '기본값'); 
-- 결과: '안녕'
```


### Oracle에서는? NVL
### 문법
```sql
NVL(값1, 값2)
```
### 예시
```sql
SELECT NVL(NULL, '기본값') FROM dual;
-- 결과: '기본값'
```
Oracle에서 IFNULL 대신 이걸 씁니다

IFNULL과 NVL은 용도는 같고 단순히 DB에 따른 문법 차이


## IFNULL, NVL과 COALESCE의 차이
> IFNULL과 NVL은 두 개의 값 중 첫 번째 값이 NULL이면 두 번째 값을 반환하는 함수이고 <br> COALESCE는 여러 개의 값 중 가장 먼저 NULL이 아닌 값을 반환하는 함수입니다