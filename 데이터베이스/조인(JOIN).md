## 📂 조인(JOIN)

✔ 여러 테이블에 저장된 데이터를 한 번에 조회해야 할 필요가 있는 경우 사용합니다.

✔ WHERE 절에 모호성을 방지하기 위해 칼럼명 앞에 테이블 명을 명시  

✔ 테이블명이 너무 긴 경우에 테이블명을 대신하는 별칭 사용  

✔ FROM 절에서 테이블명을 명시하고 공백을 둔 다음 테이블 별칭을 지정합니다.  

✔ 하나의 SQL 명령문에서 테이블명과 별명 혼용 불가능, 해당 SQL문 내에서만 유효합니다.  

```SQL
 SELECT *
   FROM EMPLOYEE, DEPARTMENT
  WHERE EMPLOYEE.DNO = DEPARTMENT.DNO
  
 -- 위 아래 SQL 명령문은 동등한 결과 출력 -- 
 
 SELECT *
   FROM EMPLOYEE e, DEPARTMENT d
  WHERE e.DNO = d.DNO;
```

### 📄 카다시안 곱
◽ 특별한 키워드 없이 SELECT 문의 FROM 절에 두 개 이상의 테이블을 콤마(,)로 연결하는 기술

<details>
<summary>🔎예제 코드 확인</summary>

```SQL
SELECT *
  FROM EMPLOYEE, DEPARTMENT;

-- 출력 결과 --
       ENO ENAME                JOB                   MANAGER HIREDATE     SALARY COMMISSION        DNO        DNO DNAME                        LOC
---------- -------------------- ------------------ ---------- -------- ---------- ---------- ---------- ---------- ---------------------------- --------------------------
      7369 SMITH                CLERK                    7902 80/12/17        800                    20         10 ACCOUNTING                   NEW YORK
      7499 ALLEN                SALESMAN                 7698 81/02/20       1600        300         30         10 ACCOUNTING                   NEW YORK
      7521 WARD                 SALESMAN                 7698 81/02/22       1250        500         30         10 ACCOUNTING                   NEW YORK
      7566 JONES                MANAGER                  7839 81/04/02       2975                    20         10 ACCOUNTING                   NEW YORK
      7654 MARTIN               SALESMAN                 7698 81/09/28       1250       1400         30         10 ACCOUNTING                   NEW YORK
      ...
```

</details>

<hr/>

### 📄 EQUI JOIN
◽ 조인 대상 테이블에서 공통 칼럼을 '='(equal) 비교를 통해 같은 값을 가지는 행을 연결

#### 📑 NATURAL JOIN

<details>
<summary>🔎자세히</summary><br>

📌 오라클에서 자동적으로 테이블의 모든 칼럼을 대상으로 일치하는 데이터 유형 및 이름을 가진 공통 칼럼을 조사한 후 자동으로 조인 수행

```SQL
 SELECT E.ENO, E.ENAME, E.JOB, E.MANAGER, E.HIREDATE, E.SALARY, E.COMMISSION, DNO
     , D.DNAME, D.LOC
   FROM EMPLOYEE E NATURAL JOIN DEPARTMENT D;
```
```SQL
 -- 급여(SAL)가 2000 초과인 사원들의 부서 정보, 사원 정보를 오른쪽과 같이 출력해 보세요
 -- 단, NATURAL JOIN 사용
 SELECT DNO, D.DNAME, E.ENO, E.ENAME, E.SALARY AS SAL
   FROM EMPLOYEE E NATURAL JOIN DEPARTMENT D
  WHERE E.SALARY > 2000;

-- 출력 결과 --
       DNO DNAME                               ENO ENAME                       SAL
---------- ---------------------------- ---------- -------------------- ----------
        10 ACCOUNTING                         7782 CLARK                      2450
        10 ACCOUNTING                         7839 KING                       5000
        20 RESEARCH                           7902 FORD                       3000
        20 RESEARCH                           7788 SCOTT                      3000
        20 RESEARCH                           7566 JONES                      2975
        30 SALES                              7698 BLAKE                      2850
```

</details>

#### 📑 JOIN ~ USING

<details>
<summary>🔎자세히</summary><br>

📌 USING 절에 조인이 대상이 되는 칼럼을 지정

```SQL
 SELECT E.ENO, E.ENAME, E.JOB, E.MANAGER, E.HIREDATE, E.SALARY, E.COMMISSION, DNO
   , D.DNAME, D.LOC
   FROM EMPLOYEE E JOIN DEPARTMENT D USING(DNO);
```
```SQL
 -- 다음 SQL문은 JOIN시 USING 키워드를 사용한 등가 조인입니다.
 -- 조건1. 사원테이블과 부서테이블의 조인 조건은 부서 번호가 같을 때입니다.
 -- 조건2. 급여는 3000 이상이며 직속상관이 반드시 있어야 합니다.
 SELECT E.ENAME, E.MANAGER, DNO, D.DNAME, D.LOC, E.SALARY
   FROM EMPLOYEE E JOIN DEPARTMENT D USING(DNO)
  WHERE E.SALARY >= 3000
    AND E.MANAGER IS NOT NULL;

-- 출력 결과 --
ENAME                   MANAGER        DNO DNAME                        LOC                            SALARY
-------------------- ---------- ---------- ---------------------------- -------------------------- ----------
FORD                       7566         20 RESEARCH                     DALLAS                           3000
SCOTT                      7566         20 RESEARCH                     DALLAS                           3000
```
```SQL
 --SQL99 이전
 -- 각 부서별 평균 급여, 최대 급여, 최소 급여, 사원 수를 출력해 보세요.
 -- 단, JOIN USING
 SELECT D.DNO, D.DNAME
      , TRUNC(AVG(E.SALARY)) AVG_SAL 
      , MAX(E.SALARY) MAX_SAL
      , MIN(E.SALARY) MIN_SAL
      , COUNT(E.ENO) CNT
   FROM EMPLOYEE E, DEPARTMENT D
  WHERE E.DNO = D.DNO
  GROUP BY D.DNO, D.DNAME;
  
 --SQL99 이후
 SELECT DNO, D.DNAME
      , TRUNC(AVG(E.SALARY)) AVG_SAL 
      , MAX(E.SALARY) MAX_SAL
      , MIN(E.SALARY) MIN_SAL
      , COUNT(E.ENO) CNT
   FROM EMPLOYEE E JOIN DEPARTMENT D USING(DNO)
  GROUP BY DNO, D.DNAME;
  
-- 출력 결과 --
       DNO DNAME                           AVG_SAL    MAX_SAL    MIN_SAL        CNT
---------- ---------------------------- ---------- ---------- ---------- ----------
        10 ACCOUNTING                         2916       5000       1300          3
        20 RESEARCH                           2175       3000        800          5
        30 SALES                              1566       2850        950          6
```

</details>

#### 📑 JOIN ~ ON

<details>
<summary>🔎자세히</summary><br>

📌 임의의 조건을 지정하거나 조인할 칼럼을 지정하려면 ON 절을 사용
```SQL
 SELECT E.ENO, E.ENAME, E.JOB, E.MANAGER, E.HIREDATE, E.SALARY, E.COMMISSION
      , E.DNO, D.DNAME, D.LOC
   FROM EMPLOYEE E JOIN DEPARTMENT D ON(E.DNO = D.DNO)
  WHERE E.SALARY >= 3000;
```
```SQL
 --SQL99 이전
 -- 모든 부서 정보와 사원 정보를 오른쪽과 같이 부서 번호, 사원 이름순으로 정렬하여 출력
 SELECT D.DNO, D.DNAME, E.ENO, E.ENAME, E.JOB, E.SALARY
   FROM EMPLOYEE E, DEPARTMENT D
  WHERE E.DNO(+) = D.DNO
  ORDER BY D.DNO, E.ENAME;
  
 --SQL99 이후
 SELECT D.DNO, D.DNAME, E.ENO, E.ENAME, E.JOB, E.SALARY
   FROM EMPLOYEE E JOIN DEPARTMENT D ON(E.DNO(+) = D.DNO)
  ORDER BY D.DNO, E.ENAME;
 
-- 출력 결과 --
       DNO DNAME                               ENO ENAME                JOB                    SALARY
---------- ---------------------------- ---------- -------------------- ------------------ ----------
        10 ACCOUNTING                         7782 CLARK                MANAGER                  2450
        10 ACCOUNTING                         7839 KING                 PRESIDENT                5000
        10 ACCOUNTING                         7934 MILLER               CLERK                    1300
        20 RESEARCH                           7876 ADAMS                CLERK                    1100
        20 RESEARCH                           7902 FORD                 ANALYST                  3000
        ...
15 rows selected.
```

</details>

<hr/>

### 📄 NON EQUI JOIN
◽ WHERE 절에 '<', BETWEEN a AND b와 같이 '=' 조건이 아닌 연산자를 사용합니다

<details>
<summary>🔎예제 코드 확인</summary>

```SQL
 SELECT *
   FROM EMPLOYEE E, SALGRADE S
  WHERE E.SALARY BETWEEN S.LOSAL AND S.HISAL;
-- 출력 결과--
       ENO ENAME                JOB                   MANAGER HIREDATE     SALARY COMMISSION        DNO      GRADE      LOSAL      HISAL
---------- -------------------- ------------------ ---------- -------- ---------- ---------- ---------- ---------- ---------- ----------
      7369 SMITH                CLERK                    7902 80/12/17        800                    20          1        700       1200
      7900 JAMES                CLERK                    7698 81/12/03        950                    30          1        700       1200
      7876 ADAMS                CLERK                    7788 87/07/13       1100                    20          1        700       1200
      7521 WARD                 SALESMAN                 7698 81/02/22       1250        500         30          2       1201       1400
      7654 MARTIN               SALESMAN                 7698 81/09/28       1250       1400         30          2       1201       1400
      7934 MILLER               CLERK                    7782 82/01/23       1300                    10          2       1201       1400
```

</details>

<hr/>

### 📄 SELF JOIN
◽ 하나의 테이블에 있는 칼럼끼리 연결해야 하는 조인이 필요한 경우 사용

<details>
<summary>🔎예제 코드 확인</summary>

```SQL
 SELECT E.ENO, E.ENAME, E.MANAGER
      , M.ENO AS MRG_ENO
      , M.ENAME AS MGR_ENAME
  FROM EMPLOYEE E, EMPLOYEE M
 WHERE E.MANAGER = M.ENO;

-- 출력 결과 --
       ENO ENAME                   MANAGER    MRG_ENO MGR_ENAME
---------- -------------------- ---------- ---------- --------------------
      7902 FORD                       7566       7566 JONES
      7788 SCOTT                      7566       7566 JONES
      7844 TURNER                     7698       7698 BLAKE
      7499 ALLEN                      7698       7698 BLAKE
      7521 WARD                       7698       7698 BLAKE
      ...
13 rows selected.
```
```SQL
SELECT E.ENO, E.ENAME, E.MANAGER
      , M.ENO, M.ENAME
   FROM EMPLOYEE E JOIN EMPLOYEE M ON(E.MANAGER = M.ENO);
   
-- 출력 결과 --
       ENO ENAME                   MANAGER        ENO ENAME
---------- -------------------- ---------- ---------- --------------------
      7902 FORD                       7566       7566 JONES
      7788 SCOTT                      7566       7566 JONES
      7844 TURNER                     7698       7698 BLAKE
      7499 ALLEN                      7698       7698 BLAKE
      7521 WARD                       7698       7698 BLAKE
      ...
13 rows selected.
```

</details>

<hr/>

### 📄 OUTER JOIN
◽ EQUI JOIN에서 양측 칼럼 값 중의 하나가 NULL이지만 조인 결과로 출력할 필요가 있는 경우 사용

#### 📑 (+) 기호를 사용한 OUTER JOIN

<details>
<summary>🔎자세히</summary>

```SQL
 SELECT D.DNO, D.DNAME, E.ENO, E.ENAME, E.JOB, E.SALARY
   FROM EMPLOYEE E, DEPARTMENT D
  WHERE E.DNO(+) = D.DNO
  ORDER BY D.DNO, E.ENAME;
  
-- 출력결과:
       DNO DNAME                 ENO ENAME      JOB           SALARY
---------- -------------- ---------- ---------- --------- ----------
        10 ACCOUNTING           7782 CLARK      MANAGER         2450
        10 ACCOUNTING           7839 KING       PRESIDENT       5000
        10 ACCOUNTING           7934 MILLER     CLERK           1300
        20 RESEARCH             7876 ADAMS      CLERK           1100
        20 RESEARCH             7902 FORD       ANALYST         3000
        20 RESEARCH             7566 JONES      MANAGER         2975
        20 RESEARCH             7788 SCOTT      ANALYST         3000
        20 RESEARCH             7369 SMITH      CLERK            800
        30 SALES                7499 ALLEN      SALESMAN        1600
        30 SALES                7698 BLAKE      MANAGER         2850
        30 SALES                7900 JAMES      CLERK            950
        30 SALES                7654 MARTIN     SALESMAN        1250
        30 SALES                7844 TURNER     SALESMAN        1500
        30 SALES                7521 WARD       SALESMAN        1250
        40 OPERATIONS                                               

```

</details>

#### 📑 ANSI OUTER JOIN(표준 조인)

<details>
<summary>🔎자세히</summary><br>

📌 ANSI 구문에서 OUTER JOIN은 LEFT OUTER JOIN, RIGHT OUTER JOIN, FULL OUTER JOIN 세 가지 타입의 조인을 제공합니다.

```SQL
 SELECT D.DNO, D.DNAME, E.ENO, E.ENAME, E.JOB, E.SALARY
   FROM EMPLOYEE E RIGHT OUTER JOIN DEPARTMENT D ON(E.DNO = D.DNO)
  ORDER BY D.DNO, E.ENAME;
  
-- 출력 결과 --
       DNO DNAME                               ENO ENAME                JOB                    SALARY
---------- ---------------------------- ---------- -------------------- ------------------ ----------
        10 ACCOUNTING                         7782 CLARK                MANAGER                  2450
        10 ACCOUNTING                         7839 KING                 PRESIDENT                5000
        10 ACCOUNTING                         7934 MILLER               CLERK                    1300
        20 RESEARCH                           7876 ADAMS                CLERK                    1100
        20 RESEARCH                           7902 FORD                 ANALYST                  3000
        20 RESEARCH                           7566 JONES                MANAGER                  2975
        20 RESEARCH                           7788 SCOTT                ANALYST                  3000
        20 RESEARCH                           7369 SMITH                CLERK                     800
        30 SALES                              7499 ALLEN                SALESMAN                 1600
        30 SALES                              7698 BLAKE                MANAGER                  2850
        30 SALES                              7900 JAMES                CLERK                     950
        30 SALES                              7654 MARTIN               SALESMAN                 1250
        30 SALES                              7844 TURNER               SALESMAN                 1500
        30 SALES                              7521 WARD                 SALESMAN                 1250
        40 OPERATIONS
```
```SQL
 -- 모든 부서 정보, 사원 정보, 급여 등급 정보, 각 사원의 직속 상관의 정보를
 -- 부서 번호, 사원 번호 순서로 정렬
 --SQL99 이전
 SELECT D.DNO, D.DNAME, E.ENO, E.ENAME, E.MANAGER, E.SALARY, E.DNO
      , S.LOSAL, S.HISAL, S.GRADE
      , M.ENO AS MGR_ENO
      , M.ENAME AS MGR_ENAME
   FROM EMPLOYEE E, EMPLOYEE M, DEPARTMENT D, SALGRADE S
  WHERE E.DNO(+) = D.DNO
        AND E.MANAGER = M.ENO(+)
        AND E.SALARY BETWEEN S.LOSAL(+) AND S.HISAL(+)
  ORDER BY D.DNO, E.ENO;
  
 --SQL99 이후
 SELECT D.DNO, D.DNAME, E.ENO, E.ENAME, E.MANAGER, E.SALARY, E.DNO
      , S.LOSAL, S.HISAL, S.GRADE
      , M.ENO AS MGR_ENO
      , M.ENAME AS MGR_ENAME
   FROM EMPLOYEE E RIGHT OUTER JOIN DEPARTMENT D ON(E.DNO = D.DNO)
        LEFT OUTER JOIN EMPLOYEE M ON(E.MANAGER = M.ENO)
        LEFT OUTER JOIN SALGRADE S ON(E.SALARY BETWEEN S.LOSAL AND S.HISAL)
  ORDER BY D.DNO, E.ENO;
-- 출력 결과 --
       DNO DNAME                               ENO ENAME                   MANAGER     SALARY        DNO      LOSAL      HISAL      GRADE    MGR_ENO MGR_ENAME
---------- ---------------------------- ---------- -------------------- ---------- ---------- ---------- ---------- ---------- ---------- ---------- --------------------
        10 ACCOUNTING                         7782 CLARK                      7839       2450         10       2001       3000          4       7839 KING
        10 ACCOUNTING                         7839 KING                                  5000         10       3001       9999          5
        10 ACCOUNTING                         7934 MILLER                     7782       1300         10       1201       1400          2       7782 CLARK
        20 RESEARCH                           7369 SMITH                      7902        800         20        700       1200          1       7902 FORD
        20 RESEARCH                           7566 JONES                      7839       2975         20       2001       3000          4       7839 KING
        20 RESEARCH                           7788 SCOTT                      7566       3000         20       2001       3000          4       7566 JONES
        20 RESEARCH                           7876 ADAMS                      7788       1100         20        700       1200          1       7788 SCOTT
        20 RESEARCH                           7902 FORD                       7566       3000         20       2001       3000          4       7566 JONES
        30 SALES                              7499 ALLEN                      7698       1600         30       1401       2000          3       7698 BLAKE
        30 SALES                              7521 WARD                       7698       1250         30       1201       1400          2       7698 BLAKE
        30 SALES                              7654 MARTIN                     7698       1250         30       1201       1400          2       7698 BLAKE
        30 SALES                              7698 BLAKE                      7839       2850         30       2001       3000          4       7839 KING
        30 SALES                              7844 TURNER                     7698       1500         30       1401       2000          3       7698 BLAKE
        30 SALES                              7900 JAMES                      7698        950         30        700       1200          1       7698 BLAKE
        40 OPERATIONS
```

</details>

<hr/>

## ✏ 정리 문제

<details>
<summary>🔎예제 코드 확인</summary>

 ```SQL
 -- 1. 사원수가 3명 이상인 부서명과 인원수 출력 (group by, having)
 SELECT D.DNAME, COUNT(*)
   FROM EMPLOYEE E, DEPARTMENT D
  WHERE E.DNO = D.DNO
  GROUP BY D.DNAME
 HAVING COUNT(*) >= 3;
 ```
 ```SQL
 -- 2~3. 사원번호, 사원이름, 부서이름, 부서번호를 출력 (Natural Join, Join On, Join Using)
 SELECT E.ENO, E.ENAME, D.DNAME, DNO
   FROM EMPLOYEE E NATURAL JOIN DEPARTMENT D;
 SELECT E.ENO, E.ENAME, D.DNAME, DNO
   FROM EMPLOYEE E JOIN DEPARTMENT D USING(DNO);
 SELECT E.ENO, E.ENAME, D.DNAME, D.DNO
   FROM EMPLOYEE E JOIN DEPARTMENT D ON(E.DNO = D.DNO);
 ```
 ```SQL
 -- 4. 부서가 30이고, 급여가 1500이상인 사원이 이름, 급여, 부서명, 부서번호를 출력하시오.
 SELECT E.ENAME, E.SALARY, D.DNAME, D.DNO
   FROM EMPLOYEE E, DEPARTMENT D
  WHERE E.SALARY >= 1500
    AND E.DNO = D.DNO
    AND E.DNO = 30;
 ```
 ```SQL
 -- 5. ADAMS 사원이 근무하는 부서이름과 지역이름을 출력하시오.
 SELECT D.DNAME, D.LOC
   FROM EMPLOYEE E, DEPARTMENT D
  WHERE E.DNO = D.DNO
    AND E.ENAME = 'ADAMS';
 ```
 ```SQL
 -- 6. NEW YORK 이나 DALLAS 지역에 근무하는 사원들의 사원번호, 사원이름을 사원번호 순으로 출력하시오.
 SELECT E.ENO, E.ENAME
   FROM EMPLOYEE E, DEPARTMENT D
  WHERE E.DNO = D.DNO
    AND D.LOC IN ('NEW YORK', 'DALLAS')
  ORDER BY E.ENAME;
 ```
 
 </details>