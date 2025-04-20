2025.04.18

학교에서 소영쌤이 연습하라고 내주신 SQL문을 기록해보려고 합니다 <br>
**틀린 부분이 있을 수도 있습니다**


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
**deptno**|deptname|floor
1|기획|8
2|개발|10
3|영업|9
4|총무|9

### employee 테이블
|사원번호|사원명|직급|월급|상사|부서코드
|:-:|:-:|:-:|:-:|:-:|:-:|
**Empno**|Empname|Title|Salary|Supervisor|dno
1001|박철수|대리|3000000|1002|1
1002|이민호|과장|3500000|1003|3
1003|김영희|부장|4000000|1006|2
1004|황진희|대리|3000000|1002|2
1005|정진우|사원|2500000|1004|1
1006|박현석|이사|5500000|null|1
1007|김정현|사원|2500000|1001|null

문제 1. 모든 사원의 직급을 중복없이 검색하세요.
```sql
select distinct title from employee;
```

문제 2. 가장 급여를 많이 받는 사원과 가장 급여를 적게 받는 사원을 검색하세요.
```sql
select * from employee where salary = (select max(salary) from employee) or salary = (select min(salary) from employee) order by salary desc;
```

문제 3. 가장 급여를 많이 받는 사람이 소속된 부서에 속한 모든 사원을 검색하세요.
```sql
select * from employee where dno = (select dno from employee where salary = (select max(salary) from employee));
```

문제 4. 모든 부서에 속한 사원의 수를 부서명과 사원수로 검색하세요.
```sql
select d.deptname, count(*) from employee e, department d where e.dno = d.deptno and e.dno is not null group by d.deptname;
```

문제 5. 8층에 있는 사원 수를 검색하세요.
```sql
select count(*) as "8층에 있는 사원수" from employee e, department d where e.dno = d.deptno and d.floor = 8
```

문제 6. 상사와 다른 부서에 속한 모든 사원의 정보를 검색하세요.
```sql
select e1.* from employee e1, employee e2 where e1.empno = e2.supervisor and e1.dno != e2.dno;
```

문제 7. 상사와 같은 부서에 속한 모든 사원의 정보를 검색하세요.
```sql
select e1.* from employee e1, employee e2 where e1.empno = e2.supervisor and e1.dno = e2.dno;
```

문제 8. 상사가 없는 사원의 모든 정보를 검색하세요.
```sql
select * from employee where supervisor is null;
```

문제 9. 월급이 15%인상한 경우 회사가 더 지급해야 하는 금액을 검색하세요.
```sql
select sum(salary)*1.15 from employee;
```

문제 10. 8층에 있는 대리의 이름, 부서명, 급여를 검색하세요.
```sql
select e.empname, d.deptname, e.salary from employee e, department d where e.dno = d.deptno and d.floor = 8;
```

문제 11. 모든 사원의 직급별 평균 급여를 검색하세요.
```sql
select title, avg(salary) from employee group by title;
```

문제 12. 기획부가 아닌 부서의 평균 급여를 검색하세요.
```sql
select avg(salary) as "기획부아닌 평균급여" from employee e, department d where e.dno = d.deptno and d.deptname != '기획';
```

문제 13. 직급별 급여 총액이 가장 큰 직급의 직급명, 평균 급여와 사원수를 검색하세요.
```sql
select title, avg(salary), count(*) from employee group by title having sum(salary) = (select max(s) from (select title, sum(salary) s from employee group by title));
```

문제 14. 모든 사원의 사원이름과 상사의 이름을 검색하세요.
```sql
select e.empname 사원, s.empname 상사 from employee e, employee s where e.supervisor = s.empno order by e.empno;
```

문제 15. 모든 직원의 사원이름과 부서 이름을 검색하세요.
```sql
select empname, deptname from employee, department where dno = deptno;
```

문제 16. 모든 직원의 사원이름과 부하직원의 이름을 검색하세요.
```sql
select e.empname 사원, s.empname 부하 from employee e, employee s where s.supervisor = e.empno order by e.empno;
```

문제 17. 기획부서나 영업부서에 속한 사원의 이름을 검색하세요.
```sql
select empname from employee, department where dno = deptno and (deptname = '기획' or deptname = '영업');
```

문제 18. 기획부서나 영업부서에 속하지 않은 사원의 이름을 검색하세요.
```sql
select empname from employee, department where dno = deptno and (deptname != '기획' and deptname != '영업');
```

문제 19. 소속 직원이 하나도 없는 부서명을 검색하세요.
```sql
select deptname from department minus select deptname from employee, department where dno = deptno;
```

다 정답인지는 잘 모르겠지만 일단 저는 13번 문제가 가장 애먹었네요..