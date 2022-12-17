# 그룹(GROUP)
## 📂 GROUP BY 절
✔ 특정 칼럼을 기준으로 그룹별로 나눌 때 사용합니다.

### 📄 GROUP BY 없이 사용할 경우
◽ 일반적으로 칼럼을 기준으로 그룹을 나눌때는 UNION(집합연산자)를 활용합니다.

<details>
<summary>🔎예제 코드 확인</summary>

```SQL
SELECT '10' AS DEPTNO, AVG(SALARY) FROM EMPLOYEE WHERE DNO = 10
 UNION
SELECT '20' AS DEPTNO, AVG(SALARY) FROM EMPLOYEE WHERE DNO = 20
 UNION
SELECT '30' AS DEPTNO, AVG(SALARY) FROM EMPLOYEE WHERE DNO = 30
 
출력:
DEPT AVG(SALARY)
---- -----------
10    2916.66667
20          2175
30    1566.66667
```

</details>

<hr/>

### 📄 GROUP BY를 사용할 경우

<details>
<summary>🔎예제 코드 확인</summary>

```SQL
 -- GROUP BY 사용
 SELECT DNO, ROUND(AVG(SALARY))
   FROM EMPLOYEE
  GROUP BY DNO
  ORDER BY DNO;
  
출력:
       DNO ROUND(AVG(SALARY))
---------- ------------------
        10               2917
        20               2175
        30               1567
```

</details>

<hr/>

### 📄 GROUP BY절을 사용할 때 유의점
◽ 다중행 함수 (SUM, AVG, MAX, MIN, COUNT)를 사용하지 않은 일반 칼럼은 GROUP BY 절에 명시해야 합니다.

<details>
<summary>🔎예제 코드 확인</summary>

```SQL
 SELECT DNO, JOB, AVG(SALARY)
   FROM EMPLOYEE
  GROUP BY DNO;

에러:
오류 발생 "not a GROUP BY expression"
오류 발생 "not a single-group group function"
```

</details>

<hr/>

## 📂 HAVING 절
✔ 표시할 그룹을 지정하여 집계 정보를 기준으로 그룹 결과를 제한합니다.

### 📄 HAVING 절을 사용한 경우

<details>
<summary>🔎예제 코드 확인</summary>

```SQL
/*
 * 각 부서의 직책별 평균 급여를 구하되 평균급여가 2000 이상인 그룹만 출력하시오
 */
 SELECT DNO, JOB, AVG(SALARY)
   FROM EMPLOYEE
  GROUP BY DNO, JOB
 HAVING AVG(SALARY) >= 2000;
 
출력:
       DNO JOB                AVG(SALARY)
---------- ------------------ -----------
        20 MANAGER                   2975
        10 PRESIDENT                 5000
        30 MANAGER                   2850
        10 MANAGER                   2450
        20 ANALYST                   3000
```

</details>

<hr/>

### 📄 WHERE 절과 HAVING 절 모두 사용한 경우

<details>
<summary>🔎예제 코드 확인</summary>

```SQL 
SELECT DNO, JOB, AVG(SALARY)
  FROM EMPLOYEE
 WHERE SALARY <= 3000
 GROUP BY DNO, JOB
HAVING AVG(SALARY) >= 2000
 ORDER BY DNO, JOB;
 
출력:
       DNO JOB                AVG(SALARY)
---------- ------------------ -----------
        10 MANAGER                   2450
        20 ANALYST                   3000
        20 MANAGER                   2975
        30 MANAGER                   2850
```

</details>

<hr/>

## 📂 그룹함수
✔ 테이블의 전체 데이터에서 통계적인 결과를 구하기 위해 행 집합에 적용하여 하나의 결과를 생성하는 함수입니다.

### 📄 SUM
◽ 그룹의 누적 합계를 반환합니다.

<details>
<summary>🔎예제 코드 확인</summary>

```SQL
SELECT SUM(COMMISSION) AS "급여", SUM(SALARY) AS "추가 수당"
  FROM EMPLOYEE;
  
출력:
      급여  추가 수당
---------- ----------
      2200      29025
```

</details>

<hr/>

### 📄 AVG
◽ 그룹의 평균을 반환합니다.

<details>
<summary>🔎예제 코드 확인</summary>

```SQL
-- 부서 번호가 30인 사람들의 평균 급여 출력하기
 SELECT AVG(SALARY)
   FROM EMPLOYEE
  WHERE DNO = 30;
  
출력:
AVG(SALARY)
-----------
 1566.66667
```

</details>

<hr/>

### 📄 COUNT
◽ 그룹의 총개수를 반환합니다.

<details>
<summary>🔎예제 코드 확인</summary>

```SQL
SELECT COUNT(DISTINCT SALARY)
     , COUNT(SALARY)
     , COUNT(ALL SALARY)
  FROM EMPLOYEE;
  
출력:
COUNT(DISTINCTSALARY) COUNT(SALARY) COUNT(ALLSALARY)
--------------------- ------------- ----------------
                   12            14               14
```

```SQL
SELECT COUNT(COMMISSION)
  FROM EMPLOYEE
 WHERE COMMISSION IS NOT NULL;
 
출력:
COUNT(COMMISSION)
-----------------
                4
```

</details>

<hr/>

### 📄 MAX
◽ 그룹의 최댓값을 반환합니다.

<details>
<summary>🔎예제 코드 확인</summary>

```SQL
 -- 부서번호가 20인 사원의 입사일 중 제일 최근 입사일 출력하기
 SELECT MAX(HIREDATE)
   FROM EMPLOYEE
  WHERE DNO = 20;
  
출력:
MAX(HIRE
--------
87/07/13
```

</details>

<hr/>

### 📄 MIN
◽ 그룹의 최솟값을 반환합니다.

<details>
<summary>🔎예제 코드 확인</summary>

```SQL
 -- 부서번호가 10번인 사원들의 최소 급여 출력하기
 SELECT MIN(SALARY)
   FROM EMPLOYEE
  WHERE DNO = 10;

출력:
MIN(SALARY)
-----------
       1300
```

</details>

<hr/>

### 📄 ROLL UP
◽ 소그룹 간의 소계를 계산합니다.

<details>
<summary>🔎예제 코드 확인</summary><br>

```SQL
 SELECT DNO, JOB, COUNT(*), MAX(SALARY), SUM(SALARY), AVG(SALARY)
   FROM EMPLOYEE
  GROUP BY ROLLUP(DNO, JOB);
  
출력:
       DNO JOB                  COUNT(*) MAX(SALARY) SUM(SALARY) AVG(SALARY)
---------- ------------------ ---------- ----------- ----------- -----------
        10 CLERK                       1        1300        1300        1300
        10 MANAGER                     1        2450        2450        2450
        10 PRESIDENT                   1        5000        5000        5000
        10                             3        5000        8750  2916.66667
        20 CLERK                       2        1100        1900         950
        20 ANALYST                     2        3000        6000        3000
        20 MANAGER                     1        2975        2975        2975
        20                             5        3000       10875        2175
        30 CLERK                       1         950         950         950
        30 MANAGER                     1        2850        2850        2850
        30 SALESMAN                    4        1600        5600        1400
        30                             6        2850        9400  1566.66667
                                      14        5000       29025  2073.21429
```

</details>

<hr/>

### 📄 CUBE
◽ GROUP BY 항목들간 다차원적인 소계를 계산할 수 있습니다.

<details>
<summary>🔎예제 코드 확인</summary><br>

```SQL
 SELECT DNO, JOB, COUNT(*), MAX(SALARY), SUM(SALARY), AVG(SALARY)
   FROM EMPLOYEE
  GROUP BY CUBE(DNO, JOB)
  ORDER BY DNO, JOB;

출력:
       DNO JOB                  COUNT(*) MAX(SALARY) SUM(SALARY) AVG(SALARY)
---------- ------------------ ---------- ----------- ----------- -----------
        10 CLERK                       1        1300        1300        1300
        10 MANAGER                     1        2450        2450        2450
        10 PRESIDENT                   1        5000        5000        5000
        10                             3        5000        8750  2916.66667
        20 ANALYST                     2        3000        6000        3000
        20 CLERK                       2        1100        1900         950
        20 MANAGER                     1        2975        2975        2975
        20                             5        3000       10875        2175
        30 CLERK                       1         950         950         950
        30 MANAGER                     1        2850        2850        2850
        30 SALESMAN                    4        1600        5600        1400
        30                             6        2850        9400  1566.66667
           ANALYST                     2        3000        6000        3000
           CLERK                       4        1300        4150      1037.5
           MANAGER                     3        2975        8275  2758.33333
           PRESIDENT                   1        5000        5000        5000
           SALESMAN                    4        1600        5600        1400
                                      14        5000       29025  2073.21429
```

</details>

<hr/>

### 📄 GROUPING SETS
◽ 같은 수준의 그룹화 열이 여러 개일때 각 열(컬럼)별 그룹화를 통해 결과 값을 출력하는데 사용함

<details>
<summary>🔎예제 코드 확인</summary><br>

```SQL
 SELECT DNO, JOB, COUNT(*)
   FROM EMPLOYEE
  GROUP BY GROUPING SETS(DNO, JOB)
  ORDER BY DNO, JOB;
  
출력:
       DNO JOB                  COUNT(*)
---------- ------------------ ----------
        10                             3
        20                             5
        30                             6
           ANALYST                     2
           CLERK                       4
           MANAGER                     3
           PRESIDENT                   1
           SALESMAN                    4
```
```SQL
 -- DECODE 문으로 GROUPING 함수를 적용하여 결과 표기하기
 SELECT DNO, JOB, COUNT(*), MAX(SALARY), SUM(SALARY), AVG(SALARY)
      , GROUPING(DNO), GROUPING(JOB)
   FROM EMPLOYEE
  GROUP BY CUBE(DNO, JOB)
  ORDER BY DNO, JOB;
  
출력:
       DNO JOB                  COUNT(*) MAX(SALARY) SUM(SALARY) AVG(SALARY) GROUPING(DNO) GROUPING(JOB)
---------- ------------------ ---------- ----------- ----------- ----------- ------------- -------------
        10 CLERK                       1        1300        1300        1300             0             0
        10 MANAGER                     1        2450        2450        2450             0             0
        10 PRESIDENT                   1        5000        5000        5000             0             0
        10                             3        5000        8750  2916.66667             0             1
        20 ANALYST                     2        3000        6000        3000             0             0
        20 CLERK                       2        1100        1900         950             0             0
        20 MANAGER                     1        2975        2975        2975             0             0
        20                             5        3000       10875        2175             0             1
        30 CLERK                       1         950         950         950             0             0
        30 MANAGER                     1        2850        2850        2850             0             0
        30 SALESMAN                    4        1600        5600        1400             0             0
        30                             6        2850        9400  1566.66667             0             1
           ANALYST                     2        3000        6000        3000             1             0
           CLERK                       4        1300        4150      1037.5             1             0
           MANAGER                     3        2975        8275  2758.33333             1             0
           PRESIDENT                   1        5000        5000        5000             1             0
           SALESMAN                    4        1600        5600        1400             1             0
                                      14        5000       29025  2073.21429             1             1
```
```SQL
 -- DECODE 문으로 GROUPING 함수를 적용하여 결과 표기하기
 SELECT DECODE(GROUPING(DNO), 1, DECODE(GROUPING(JOB), 1 , '총계', 'ALL'), DNO) AS DNO
      , DECODE(GROUPING(JOB), 1, DECODE(GROUPING(DNO), 1 , ' ', '소계'), JOB) AS JOB
      , COUNT(*), MAX(SALARY), SUM(SALARY), ROUND(AVG(SALARY)), GROUPING(DNO), GROUPING(JOB)
   FROM EMPLOYEE
  GROUP BY CUBE(DNO, JOB)
  ORDER BY DNO, JOB;
  
출력:
DNO                                                                              JOB                  COUNT(*) MAX(SALARY) SUM(SALARY) ROUND(AVG(SALARY)) GROUPING(DNO) GROUPING(JOB)
-------------------------------------------------------------------------------- ------------------ ---------- ----------- ----------- ------------------ ------------- -------------
10                                                                               CLERK                       1        1300        1300               1300             0             0
10                                                                               MANAGER                     1        2450        2450               2450             0             0
10                                                                               PRESIDENT                   1        5000        5000               5000             0             0
10                                                                               소계                        3        5000        8750               2917             0             1
20                                                                               ANALYST                     2        3000        6000               3000             0             0
20                                                                               CLERK                       2        1100        1900                950             0             0
20                                                                               MANAGER                     1        2975        2975               2975             0             0
20                                                                               소계                        5        3000       10875               2175             0             1
30                                                                               CLERK                       1         950         950                950             0             0
30                                                                               MANAGER                     1        2850        2850               2850             0             0
30                                                                               SALESMAN                    4        1600        5600               1400             0             0
30                                                                               소계                        6        2850        9400               1567             0             1
ALL                                                                              ANALYST                     2        3000        6000               3000             1             0
ALL                                                                              CLERK                       4        1300        4150               1038             1             0
ALL                                                                              MANAGER                     3        2975        8275               2758             1             0
ALL                                                                              PRESIDENT                   1        5000        5000               5000             1             0
ALL                                                                              SALESMAN                    4        1600        5600               1400             1             0
총계                                                                                                        14        5000       29025               2073             1             1
```

</details>

<hr/>

### 📄 LISTAGG
◽ 그룹을 만들고 그룹이 되지 않은 나열하고 싶은 칼럼을 반환합니다.

<details>
<summary>🔎예제 코드 확인</summary><br>

```SQL
 -- LISTAGG 함수(오라클 11G 이상)
 SELECT DNO
      , LISTAGG(ENAME, ', ')
        WITHIN GROUP(ORDER BY SALARY DESC) AS ENAMES
   FROM EMPLOYEE
  GROUP BY DNO;
  
출력:
ENAMES
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
        10
KING, CLARK, MILLER

        20
FORD, SCOTT, JONES, ADAMS, SMITH

        30
BLAKE, ALLEN, TURNER, MARTIN, WARD, JAMES
```

</details>

<hr/>

### 📄 PIVOT
◽ 로우 단위를 칼럼 단위로 변경해줍니다.

<details>
<summary>🔎예제 코드 확인</summary><br>

```SQL
-- PIVOT 함수를 사용하여 직책별, 부서별 최고 급여를 2차원 표 형태로 출력하기
 SELECT *
   FROM (SELECT DNO, JOB, SALARY
           FROM EMPLOYEE)
  PIVOT(MAX(SALARY)
        FOR DNO IN (10, 20, 30)
       )
  ORDER BY JOB;
  
출력:
JOB                        10         20         30
------------------ ---------- ---------- ----------
ANALYST                             3000
CLERK                    1300       1100        950
MANAGER                  2450       2975       2850
PRESIDENT                5000
SALESMAN                                       1600
```
```SQL
 -- PIVOT 함수를 사용하여 부서별, 직책별 최고 급여를 2 차원 표 형태로 출력
 SELECT *
   FROM (SELECT JOB, DNO, SALARY
           FROM EMPLOYEE)
  PIVOT(MAX(SALARY)
        FOR JOB IN ('CLERK' AS CLERK,
                 'SALESMAN' AS SALESMAN,
                'PRESIDENT' AS PRESIDENT,
                  'MANAGER' AS MANAGER,
                  'ANALYST' AS ANALYST)
       )
 ORDER BY DNO;
 
출력:
       DNO      CLERK   SALESMAN  PRESIDENT    MANAGER    ANALYST
---------- ---------- ---------- ---------- ---------- ----------
        10       1300                  5000       2450
        20       1100                             2975       3000
        30        950       1600                  2850
```

</details>

<hr/>

## ✏ 정리 문제

<details>
<summary>🔎예제 코드 확인</summary><br>

```SQL
 -- 각 부서의 입사 연도별 사원 수, 최고 급여, 급여 합, 평균 급여를 출력하고
 -- 각 부서별 소계와 총계를 출력하세요.
 SELECT DECODE(GROUPING(DNO), 1, DECODE(GROUPING(TO_CHAR(HIREDATE, 'YYYY')), 1, 'ALL'), DNO) AS DNO
      , DECODE(GROUPING(TO_CHAR(HIREDATE, 'YYYY')), 1
      , DECODE(GROUPING(DNO), 1, '총계', '소계'), TO_CHAR(HIREDATE, 'YYYY')) AS HIRE_YEAR
      , COUNT(*) AS CNT
      , MAX(SALARY) AS MAX_SAL
      , SUM(SALARY) AS SUM_SAL
      , TRUNC(AVG(SALARY)) AS AVG_SAL
   FROM EMPLOYEE
  GROUP BY ROLLUP(DNO, TO_CHAR(HIREDATE, 'YYYY'));
  
출력:
DNO                                                                              HIRE_YEAR           CNT    MAX_SAL    SUM_SAL    AVG_SAL
-------------------------------------------------------------------------------- ------------ ---------- ---------- ---------- ----------
10                                                                               1981                  2       5000       7450       3725
10                                                                               1982                  1       1300       1300       1300
10                                                                               소계                  3       5000       8750       2916
20                                                                               1980                  1        800        800        800
20                                                                               1981                  2       3000       5975       2987
20                                                                               1987                  2       3000       4100       2050
20                                                                               소계                  5       3000      10875       2175
30                                                                               1981                  6       2850       9400       1566
30                                                                               소계                  6       2850       9400       1566
ALL                                                                              총계                 14       5000      29025       2073
```

</details>
