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


## RANK( ) vs DENSE_RANK( ) vs ROW_NUMBER( )