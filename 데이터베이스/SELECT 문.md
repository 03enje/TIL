```sql
SELECT [DISTINCT] {*, column[Alias], ...}
FROM table_name
[WHERE condition]
[GROUP BY group_by_expression]
[Having group_condition]
[ORDER BY column]
```

|절|기능|
|------|------|
|SELECT 절|조회하고자 하는 칼럼명의 리스트를 나열합니다.|
|DISTINCT 절|동일한 내용을 한 번씩만 출력하여 중복을 제거합니다.|
|FROM 절|조회하고자 하는 테이블명의 리스트를 나열합니다.|
|WHERE 절|조회하고자 하는 로우의 조건을 나열합니다.|
|GROUP BY 절|동일한 값을 갖는 로우들을 한 그룹으로 묶습니다.|
|HAVING 절|로우들의 그룹이 만족해야 하는 조건을 제시합니다.|
|ORDER BY 절|로우들의 정렬 순서를 제시합니다. [ASC] = 오름차순, [DESC] = 내림차순|
```sql
SELECT *
FROM EMP;
```
- SELECT는 데이터베이스 내에 저장되어있는 테이블을 조회하기 위한
명령어입니다.

- SELECT 다음에는 보고자 하는 대상의 칼럼명을 기술합니다. SELECT 
다음에 *을 기술하면 지정된 테이블의 모든 칼럼을 조회합니다. 

- FROM 다음에는 보고자 하는 대상의 테이블 이름을 기술합니다.

## nvl 함수
NULL, ? 은 ∞의 의미이기 때문에 연산, 할당, 비교가 불가능합니다.
```sql
select ename, salary, job, dno, commission, 
salary*12, salary*12+commission
from employee;

출력: 
ENAME                    SALARY JOB                       DNO COMMISSION  SALARY*12 SALARY*12+COMMISSION
-------------------- ---------- ------------------ ---------- ---------- ---------- --------------------
SMITH                       800 CLERK                      20                  9600
ALLEN                      1600 SALESMAN                   30        300      19200                19500
```
> COMMISSION에 NULL값이 들어가 연산 불가능
```sql
select ename, salary, job, dno, nvl(commission, 0), 
salary*12, salary*12+nvl(commission, 0)
from employee;

출력:
ENAME                    SALARY JOB                       DNO NVL(COMMISSION,0)  SALARY*12 SALARY*12+NVL(COMMISSION,0)
-------------------- ---------- ------------------ ---------- ----------------- ---------- ---------------------------
SMITH                       800 CLERK                      20                 0       9600                        9600
ALLEN                      1600 SALESMAN                   30               300      19200                       19500
```
> nvl을 사용하여 NULL값을 0으로 처리
