# 오라클 * Plus

## SQL*Plus
- SQL 문을 대화식으로 실행하기 위해서 사용자가 데이터베이스에 입력하고 SQL 문을 처리하여 그 결가를 받을 수 있도록 만든 툴 (오라클 콘솔)
## SQL(Structured Query Language)
- 테이블을 저장 단위로 생각하는 관계형 데이터베이스(Relational Data Base: RDB)를 처리(저장, 수정, 삭제, 추출)하기 위해 미국표준협회(ANSI)에서 표준으로 채택한 언어

C:\oraclexe\app\oracle\product\11.2.0\server\sqlplus\admin -> glogin 메모장 실행 -> 

> set linesize 300
>
> set pagesize 100
     
마지막에 저장

- 명령어 desc employee (테이블 정렬)

## SELECT 명령어
SELECTION 행을 가져옴
PROJECTION 열을 가져옴
JOIN 2개의 테이블을 연결함

SELECT (조회할 컬럼) FROM (조회할 테이블)
> 추가 명령어 * (전체 선택)

SELECT DISTINCT DNO FROM EMPOLYEE 
> DISTINCT -> 중복 제거

Alias
사용 방법
> 가공 문장 이후 AS 별칭
SELECT ENAME, SALARY, SALARY*12+COMMISSION AS ANNSAL, COMMISSION FROM EMPLOYEE;

별칭 전
ENAME                    SALARY SALARY*12+COMMISSION COMMISSION
-------------------- ---------- -------------------- ----------
SMITH                       800
ALLEN                      1600                19500        300

별칭 후
ENAME                    SALARY     ANNSAL COMMISSION
-------------------- ---------- ---------- ----------
SMITH                       800
ALLEN                      1600      19500        300

> ORDER BY 내림차순 DESC
SELECT * FROM EMPLOYEE ORDER BY SALARY DESC;
```sql
ENO ENAME                JOB                   MANAGER HIREDATE     SALARY COMMISSION        DNO
---------- -------------------- ------------------ ---------- -------- ---------- ---------- ----------
      7839 KING                 PRESIDENT                     81/11/17       5000                    10
      7902 FORD                 ANALYST                  7566 81/12/03       3000                    20
      7788 SCOTT                ANALYST                  7566 87/07/13       3000                    20
      7566 JONES                MANAGER                  7839 81/04/02       2975                    20
```
> ORDER BY 내림차순 DESC 오름차순 ASC
SELECT * FROM EMPLOYEE ORDER BY DNO ASC, SALARY DESC; -> ORDER BY는 먼저 입력순으로
```sql
       ENO ENAME                JOB                   MANAGER HIREDATE     SALARY COMMISSION        DNO
---------- -------------------- ------------------ ---------- -------- ---------- ---------- ----------
      7839 KING                 PRESIDENT                     81/11/17       5000                    10
      7782 CLARK                MANAGER                  7839 81/06/09       2450                    10
      7934 MILLER               CLERK                    7782 82/01/23       1300                    10
```
RUN, LIST

- 메모장 키는 명령어 ed -> 버퍼에 저장된 쿼리

  1  SELECT ename, salary*12+nvl(commission, 0) as annsal
  2   FROM EMPLOYEE
  3* ORDER BY DNO ASC, SALARY DESC
  
  메모장에 저장 후 / 입력하여 실행
  
SQL> save sample (host에 sql저장)
Created file sample.sql

SQL> host (sql이 저장되는 경로)
Microsoft Windows [Version 10.0.19044.2251]
(c) Microsoft Corporation. All rights reserved.

C:\oraclexe\app\oracle\product\11.2.0\server\BIN> dir s* (s로 시작하는 모든 파일)
2022-11-24  오전 11:51               104 sample.sql

SQL> @sample

```sql
ENAME                    ANNSAL
-------------------- ----------
KING                      60000
CLARK                     29400
MILLER                    15600
```

SQL> SET HEADING OFF
SQL> SET PAGESIZE 50000
SQL> SET COLSEP '|'
SQL> SPOOL C:\oraclexe\app\oracle\product\11.2.0\server\BIN\test.txt
SQL> SELECT * FROM DEPARTMENT;

SQL> SELECT * FROM DEPARTMENT;
```sql
        10|ACCOUNTING                  |NEW YORK
        20|RESEARCH                    |DALLAS
        30|SALES                       |CHICAGO
        40|OPERATIONS                  |BOSTON
```        
SQL> SPOOL OFF

SQL> SET HEADING ON
```sql
       ENO|ENAME               |JOB               |   MANAGER|HIREDATE|    SALARY|COMMISSION|       DNO
----------|--------------------|------------------|----------|--------|----------|----------|----------
      7369|SMITH               |CLERK             |      7902|80/12/17|       800|          |        20
      7499|ALLEN               |SALESMAN          |      7698|81/02/20|      1600|       300|        30
```