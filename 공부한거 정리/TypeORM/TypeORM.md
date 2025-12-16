2025.03.05

## ORM(Object-Relational Mapping)이란?

ORM은 **객체(Object)와 관계형 데이터베이스(Relational Database)** 를 매핑하는 기술 <br>
일반적으로 SQL 쿼리를 직접 작성하는 대신, 클래스를 사용하여 데이터베이스와 상호작용할 수 있도록 도와줌
### 장점
1. SQL을 직접 작성할 필요 없이 객체 기반으로 데이터 조작 가능
2. DB 변경 시 코드 수정이 최소화됨
3. 보안성 향상 (SQL Injection 방지)
4. DBMS(MySQL, PostgreSQL, SQLite 등) 교체가 용이함
### 단점
1. 사용하기는 편하지만 설계는 매우 신중하게 해야함
2. 프로젝트의 복잡성이 커질 경우 난이도 또한 올라갈 수 있음
3. 잘못 구현된 경우에 속도 저하 및 심각할 경우 일관성이 무너지는 문제점이 생길수 있음
4. 이미 [프로시저](/2025/프로시저.md)가 많은 시스템에서는 다시 객체로 바꿔야함, 그 과정에서 생산성 저하나 리스크가 많이 발생할 수 있음
<br><br>

## TypeORM

TypeORM은 TypeScript 및 JavaScript(ES6 이상)에서 사용할 수 있는 객체 관계 매핑(Object-Relational Mapping, ORM) 라이브러리이다 

예제 이미지)
![alt text](https://velog.velcdn.com/images/tilto0822/post/521327bc-fbee-4708-b4e6-3be5761e1da1/image.png)