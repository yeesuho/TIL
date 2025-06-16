2025.06.16

ALTER 문은 SQL에서 기존 테이블의 구조(스키마)를 수정할 때 사용하는 명령어입니다

컬럼을 추가하거나 삭제하거나, 이름을 바꾸거나, 자료형을 변경할 때 쓰죠

### 컬럼 추가 (ADD)
```sql
ALTER TABLE 테이블명
ADD 컬럼명 데이터타입;
```
예)
```sql
ALTER TABLE member_tbl
ADD phone VARCHAR2(20);
```

### 컬럼 삭제 (DROP)
```sql
ALTER TABLE 테이블명
DROP COLUMN 컬럼명;
```
예)
```sql
ALTER TABLE member_tbl
DROP COLUMN phone;
```

### 컬럼 이름 변경 (RENAME COLUMN)
```sql
ALTER TABLE 테이블명
RENAME COLUMN 기존컬럼명 TO 새컬럼명;
```
예)
```sql
ALTER TABLE member_tbl
RENAME COLUMN phone TO phone_number;
```

### 컬럼 데이터 타입 변경 (MODIFY)
```sql
ALTER TABLE 테이블명
MODIFY 컬럼명 새데이터타입;
```
예)
```sql
ALTER TABLE member_tbl
MODIFY phone_number VARCHAR2(30);
```

### 테이블 이름 변경
```sql
RENAME 기존테이블명 TO 새테이블명;
```
예)
```sql
RENAME member_tbl TO customer_tbl;
```