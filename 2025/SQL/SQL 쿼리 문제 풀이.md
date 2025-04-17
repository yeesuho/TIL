2025.04.18

학교에서 소영쌤이 연습하라고 내주신 SQL문을 기록해보려고 한다


테이블 추가
``` sql
suho.sql
create table department
(
    deptno number primary key,
    deptname varchar(10),
    floor number
);

create table employee
(
    empno number primary key,
    empname varchar2(10),
    title varchar2(10),
    salary number(8),
    supervisor number,
    dno number
);


insert into department
(deptno, deptname, floor)
values (1, '기획', 8 );

insert into department
values
(2, '개발', 10);

insert into department
values
(3, '영업', 9);

insert into department
values
(4, '총무', 9);

select * from employee;

insert into employee
values
(1001, '박철수', '대리', 3000000, 1002, 1);

insert into employee
values
(1002, '이민호', '과장', 3500000, 1003, 3);

insert into employee
values
(1003, '김영희', '부장', 4000000, 1006, 2);

insert into employee
values
(1004, '황진희', '대리', 3000000, 1002, 2);

insert into employee
values
(1005, '정진우', '사원', 2500000, 1004, 1);

insert into employee
values
(1006, '박현석', '이사', 5500000, null, 1);

insert into employee
values
(1007, '김정현', '사원', 2500000, 1001, null);
```

### department 테이블
|부서번호|부서이름|위치|
|:-:|:-:|:-:|
|deptno|deptname|floor
1|
2|
3|
4|

### employee 테이블



문제 1. 모든 사원의 직급을 중복없이 검색하세요.
```sql
select distinct title from employee;
```