2025.06.15

**시퀀스(Sequence)** 는 자동으로 숫자를 생성해주는 객체입니다

보통 **기본키(PK)** 처럼 자동 증가값이 필요할 때 씁니다 (예: 회원번호, 주문번호)

### 시퀀스는
순차적으로 숫자를 자동 생성하는 오라클(Oracle) 등의 데이터베이스 객체<br>
INSERT할 때 일일이 번호 안 써도 되니까 아주 편합니다

### 시퀀스 생성하기 (Oracle 기준)
```sql
CREATE SEQUENCE 시퀀스이름
START WITH 1       -- 시작값
INCREMENT BY 1     -- 증가값
MINVALUE 1         -- 최소값
MAXVALUE 99999     -- 최대값
CYCLE              -- 최대값 도달하면 다시 최소값으로 순환 (옵션)
NOCACHE;           -- 캐시 안 함 (기본값은 CACHE 20)
```


### 시퀀스 사용하기 (INSERT 시)
```sql
INSERT INTO member_tbl (
  cust_no, name, phone, address, joindate, point, grade
)
VALUES (
  member_seq.NEXTVAL,  -- 자동 증가값
  '이정재',
  '01012345678',
  '서울시 용산구',
  TO_CHAR(SYSDATE, 'YYYYMMDD'),
  0,
  '02'
);
```
- `NEXTVAL`: 다음 숫자 반환 (값 증가됨)

- `CURRVAL`: 최근에 사용한 숫자 확인 (같은 세션 내에서)

### 시퀀스 조회
```sql
SELECT member_seq.CURRVAL FROM dual;
```
- 바로 NEXTVAL을 사용하지 않고 CURRVAL만 쓰면 에러납니다
→ NEXTVAL을 먼저 호출해야 CURRVAL 사용 가능해

### 시퀀스 삭제
```sql
DROP SEQUENCE member_seq;
```