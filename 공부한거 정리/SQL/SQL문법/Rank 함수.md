2025.05.31

RANK는 **순위(등수)**를 구할 때 사용하는 함수 중 하나입니다
<br>
ORDER BY와 함께 사용해서 원하는 기준으로 순위를 매길 수 있죠


## RANK( ) 함수란?
RANK()는 동일한 값이 있을 경우 동일한 순위를 부여하고 그 다음 순위는 건너뛰는 순위 함수입니다

### 기본 문법
```sql
SELECT 컬럼들, RANK() OVER (PARTITION BY 그룹컬럼 ORDER BY 정렬기준컬럼 ASC|DESC) AS 순위
FROM 테이블명;
```


### 예제 테이블: score_tbl
가상의 예제 테이블로 예를 들어보겠습니다

|name|subject|score
|:-:|:-:|:-:|
Alice|Math|90
Bob|Math|80
Carol|Math|90
David|Math|70
Erin|Math|60


## 기본 사용 예시

```sql
SELECT name, score,
       RANK() OVER (ORDER BY score DESC) AS rank
FROM score_tbl;
```
### 결과:
|name|score|rank
|:-:|:-:|:-:|
Alice|90|1
Carol|90|1
Bob|80|3
David|70|4
Erin|60|5

Alice와 Carol은 같은 점수 => 같은 순위 1위<br>
그 다음은 3위 (2위는 건너뜀)

2025.06.01
## RANK( ) vs DENSE_RANK( ) vs ROW_NUMBER( )
|함수명|동순위 처리|다음 순위
|:-:|:-:|:-:|
RANK()|동순위 있음|순위 건너뜀
DENSE_RANK()|동순위 있음|순위 안 건너뜀
ROW_NUMBER()|무조건 고유|1, 2, 3...
```sql
SELECT name, score,
       RANK() OVER (ORDER BY score DESC)         AS rank,
       DENSE_RANK() OVER (ORDER BY score DESC)   AS dense_rank,
       ROW_NUMBER() OVER (ORDER BY score DESC)   AS row_num
FROM score_tbl;
```
### 결과:
name|score|rank|dense_rank|row_num
|:-:|:-:|:-:|:-:|:-:|
Alice|90|1|1|1
Carol|90|1|1|2
Bob|80|3|2|3
David|70|4|3|4
Erin|60|5|4|5


## PARTITION BY로 그룹별 순위 매기기
```sql  
SELECT name, subject, score,
       RANK() OVER (PARTITION BY subject ORDER BY score DESC) AS subject_rank
FROM score_tbl;
```
과목별로 그룹을 나누고 그 안에서 순위 부여

## 요약
항목|설명
|:-:|:-:|
RANK()|같은 값엔 같은 순위, 그 다음은 건너뜀 (ex: 1, 1, 3)
DENSE_RANK()|같은 값엔 같은 순위, 그 다음은 바로 다음 순위 (ex: 1, 1, 2)
ROW_NUMBER()|같은 값이어도 고유한 순위 부여 (ex: 1, 2, 3)
OVER(ORDER BY)|정렬 기준을 지정
PARTITION BY|그룹을 나누고 각 그룹별로 순위를 부여