# ๊ทธ๋ฃน(GROUP)
## ๐ GROUP BY ์ 
โ ํน์  ์นผ๋ผ์ ๊ธฐ์ค์ผ๋ก ๊ทธ๋ฃน๋ณ๋ก ๋๋ ๋ ์ฌ์ฉํฉ๋๋ค.

### ๐ GROUP BY ์์ด ์ฌ์ฉํ  ๊ฒฝ์ฐ
โฝ ์ผ๋ฐ์ ์ผ๋ก ์นผ๋ผ์ ๊ธฐ์ค์ผ๋ก ๊ทธ๋ฃน์ ๋๋๋๋ UNION(์งํฉ์ฐ์ฐ์)๋ฅผ ํ์ฉํฉ๋๋ค.

<details>
<summary>๐์์  ์ฝ๋ ํ์ธ</summary>

```SQL
SELECT '10' AS DEPTNO, AVG(SALARY) FROM EMPLOYEE WHERE DNO = 10
 UNION
SELECT '20' AS DEPTNO, AVG(SALARY) FROM EMPLOYEE WHERE DNO = 20
 UNION
SELECT '30' AS DEPTNO, AVG(SALARY) FROM EMPLOYEE WHERE DNO = 30
 
์ถ๋ ฅ:
DEPT AVG(SALARY)
---- -----------
10    2916.66667
20          2175
30    1566.66667
```

</details>

<hr/>

### ๐ GROUP BY๋ฅผ ์ฌ์ฉํ  ๊ฒฝ์ฐ

<details>
<summary>๐์์  ์ฝ๋ ํ์ธ</summary>

```SQL
 -- GROUP BY ์ฌ์ฉ
 SELECT DNO, ROUND(AVG(SALARY))
   FROM EMPLOYEE
  GROUP BY DNO
  ORDER BY DNO;
  
์ถ๋ ฅ:
       DNO ROUND(AVG(SALARY))
---------- ------------------
        10               2917
        20               2175
        30               1567
```

</details>

<hr/>

### ๐ GROUP BY์ ์ ์ฌ์ฉํ  ๋ ์ ์์ 
โฝ ๋ค์คํ ํจ์ (SUM, AVG, MAX, MIN, COUNT)๋ฅผ ์ฌ์ฉํ์ง ์์ ์ผ๋ฐ ์นผ๋ผ์ GROUP BY ์ ์ ๋ช์ํด์ผ ํฉ๋๋ค.

<details>
<summary>๐์์  ์ฝ๋ ํ์ธ</summary>

```SQL
 SELECT DNO, JOB, AVG(SALARY)
   FROM EMPLOYEE
  GROUP BY DNO;

์๋ฌ:
์ค๋ฅ ๋ฐ์ "not a GROUP BY expression"
์ค๋ฅ ๋ฐ์ "not a single-group group function"
```

</details>

<hr/>

## ๐ HAVING ์ 
โ ํ์ํ  ๊ทธ๋ฃน์ ์ง์ ํ์ฌ ์ง๊ณ ์ ๋ณด๋ฅผ ๊ธฐ์ค์ผ๋ก ๊ทธ๋ฃน ๊ฒฐ๊ณผ๋ฅผ ์ ํํฉ๋๋ค.

### ๐ HAVING ์ ์ ์ฌ์ฉํ ๊ฒฝ์ฐ

<details>
<summary>๐์์  ์ฝ๋ ํ์ธ</summary>

```SQL
/*
 * ๊ฐ ๋ถ์์ ์ง์ฑ๋ณ ํ๊ท  ๊ธ์ฌ๋ฅผ ๊ตฌํ๋ ํ๊ท ๊ธ์ฌ๊ฐ 2000 ์ด์์ธ ๊ทธ๋ฃน๋ง ์ถ๋ ฅํ์์ค
 */
 SELECT DNO, JOB, AVG(SALARY)
   FROM EMPLOYEE
  GROUP BY DNO, JOB
 HAVING AVG(SALARY) >= 2000;
 
์ถ๋ ฅ:
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

### ๐ WHERE ์ ๊ณผ HAVING ์  ๋ชจ๋ ์ฌ์ฉํ ๊ฒฝ์ฐ

<details>
<summary>๐์์  ์ฝ๋ ํ์ธ</summary>

```SQL 
SELECT DNO, JOB, AVG(SALARY)
  FROM EMPLOYEE
 WHERE SALARY <= 3000
 GROUP BY DNO, JOB
HAVING AVG(SALARY) >= 2000
 ORDER BY DNO, JOB;
 
์ถ๋ ฅ:
       DNO JOB                AVG(SALARY)
---------- ------------------ -----------
        10 MANAGER                   2450
        20 ANALYST                   3000
        20 MANAGER                   2975
        30 MANAGER                   2850
```

</details>

<hr/>

## ๐ ๊ทธ๋ฃนํจ์
โ ํ์ด๋ธ์ ์ ์ฒด ๋ฐ์ดํฐ์์ ํต๊ณ์ ์ธ ๊ฒฐ๊ณผ๋ฅผ ๊ตฌํ๊ธฐ ์ํด ํ ์งํฉ์ ์ ์ฉํ์ฌ ํ๋์ ๊ฒฐ๊ณผ๋ฅผ ์์ฑํ๋ ํจ์์๋๋ค.

### ๐ SUM
โฝ ๊ทธ๋ฃน์ ๋์  ํฉ๊ณ๋ฅผ ๋ฐํํฉ๋๋ค.

<details>
<summary>๐์์  ์ฝ๋ ํ์ธ</summary>

```SQL
SELECT SUM(COMMISSION) AS "๊ธ์ฌ", SUM(SALARY) AS "์ถ๊ฐ ์๋น"
  FROM EMPLOYEE;
  
์ถ๋ ฅ:
      ๊ธ์ฌ  ์ถ๊ฐ ์๋น
---------- ----------
      2200      29025
```

</details>

<hr/>

### ๐ AVG
โฝ ๊ทธ๋ฃน์ ํ๊ท ์ ๋ฐํํฉ๋๋ค.

<details>
<summary>๐์์  ์ฝ๋ ํ์ธ</summary>

```SQL
-- ๋ถ์ ๋ฒํธ๊ฐ 30์ธ ์ฌ๋๋ค์ ํ๊ท  ๊ธ์ฌ ์ถ๋ ฅํ๊ธฐ
 SELECT AVG(SALARY)
   FROM EMPLOYEE
  WHERE DNO = 30;
  
์ถ๋ ฅ:
AVG(SALARY)
-----------
 1566.66667
```

</details>

<hr/>

### ๐ COUNT
โฝ ๊ทธ๋ฃน์ ์ด๊ฐ์๋ฅผ ๋ฐํํฉ๋๋ค.

<details>
<summary>๐์์  ์ฝ๋ ํ์ธ</summary>

```SQL
SELECT COUNT(DISTINCT SALARY)
     , COUNT(SALARY)
     , COUNT(ALL SALARY)
  FROM EMPLOYEE;
  
์ถ๋ ฅ:
COUNT(DISTINCTSALARY) COUNT(SALARY) COUNT(ALLSALARY)
--------------------- ------------- ----------------
                   12            14               14
```

```SQL
SELECT COUNT(COMMISSION)
  FROM EMPLOYEE
 WHERE COMMISSION IS NOT NULL;
 
์ถ๋ ฅ:
COUNT(COMMISSION)
-----------------
                4
```

</details>

<hr/>

### ๐ MAX
โฝ ๊ทธ๋ฃน์ ์ต๋๊ฐ์ ๋ฐํํฉ๋๋ค.

<details>
<summary>๐์์  ์ฝ๋ ํ์ธ</summary>

```SQL
 -- ๋ถ์๋ฒํธ๊ฐ 20์ธ ์ฌ์์ ์์ฌ์ผ ์ค ์ ์ผ ์ต๊ทผ ์์ฌ์ผ ์ถ๋ ฅํ๊ธฐ
 SELECT MAX(HIREDATE)
   FROM EMPLOYEE
  WHERE DNO = 20;
  
์ถ๋ ฅ:
MAX(HIRE
--------
87/07/13
```

</details>

<hr/>

### ๐ MIN
โฝ ๊ทธ๋ฃน์ ์ต์๊ฐ์ ๋ฐํํฉ๋๋ค.

<details>
<summary>๐์์  ์ฝ๋ ํ์ธ</summary>

```SQL
 -- ๋ถ์๋ฒํธ๊ฐ 10๋ฒ์ธ ์ฌ์๋ค์ ์ต์ ๊ธ์ฌ ์ถ๋ ฅํ๊ธฐ
 SELECT MIN(SALARY)
   FROM EMPLOYEE
  WHERE DNO = 10;

์ถ๋ ฅ:
MIN(SALARY)
-----------
       1300
```

</details>

<hr/>

### ๐ ROLL UP
โฝ ์๊ทธ๋ฃน ๊ฐ์ ์๊ณ๋ฅผ ๊ณ์ฐํฉ๋๋ค.

<details>
<summary>๐์์  ์ฝ๋ ํ์ธ</summary><br>

```SQL
 SELECT DNO, JOB, COUNT(*), MAX(SALARY), SUM(SALARY), AVG(SALARY)
   FROM EMPLOYEE
  GROUP BY ROLLUP(DNO, JOB);
  
์ถ๋ ฅ:
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

### ๐ CUBE
โฝ GROUP BY ํญ๋ชฉ๋ค๊ฐ ๋ค์ฐจ์์ ์ธ ์๊ณ๋ฅผ ๊ณ์ฐํ  ์ ์์ต๋๋ค.

<details>
<summary>๐์์  ์ฝ๋ ํ์ธ</summary><br>

```SQL
 SELECT DNO, JOB, COUNT(*), MAX(SALARY), SUM(SALARY), AVG(SALARY)
   FROM EMPLOYEE
  GROUP BY CUBE(DNO, JOB)
  ORDER BY DNO, JOB;

์ถ๋ ฅ:
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

### ๐ GROUPING SETS
โฝ ๊ฐ์ ์์ค์ ๊ทธ๋ฃนํ ์ด์ด ์ฌ๋ฌ ๊ฐ์ผ๋ ๊ฐ ์ด(์ปฌ๋ผ)๋ณ ๊ทธ๋ฃนํ๋ฅผ ํตํด ๊ฒฐ๊ณผ ๊ฐ์ ์ถ๋ ฅํ๋๋ฐ ์ฌ์ฉํจ

<details>
<summary>๐์์  ์ฝ๋ ํ์ธ</summary><br>

```SQL
 SELECT DNO, JOB, COUNT(*)
   FROM EMPLOYEE
  GROUP BY GROUPING SETS(DNO, JOB)
  ORDER BY DNO, JOB;
  
์ถ๋ ฅ:
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
 -- DECODE ๋ฌธ์ผ๋ก GROUPING ํจ์๋ฅผ ์ ์ฉํ์ฌ ๊ฒฐ๊ณผ ํ๊ธฐํ๊ธฐ
 SELECT DNO, JOB, COUNT(*), MAX(SALARY), SUM(SALARY), AVG(SALARY)
      , GROUPING(DNO), GROUPING(JOB)
   FROM EMPLOYEE
  GROUP BY CUBE(DNO, JOB)
  ORDER BY DNO, JOB;
  
์ถ๋ ฅ:
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
 -- DECODE ๋ฌธ์ผ๋ก GROUPING ํจ์๋ฅผ ์ ์ฉํ์ฌ ๊ฒฐ๊ณผ ํ๊ธฐํ๊ธฐ
 SELECT DECODE(GROUPING(DNO), 1, DECODE(GROUPING(JOB), 1 , '์ด๊ณ', 'ALL'), DNO) AS DNO
      , DECODE(GROUPING(JOB), 1, DECODE(GROUPING(DNO), 1 , ' ', '์๊ณ'), JOB) AS JOB
      , COUNT(*), MAX(SALARY), SUM(SALARY), ROUND(AVG(SALARY)), GROUPING(DNO), GROUPING(JOB)
   FROM EMPLOYEE
  GROUP BY CUBE(DNO, JOB)
  ORDER BY DNO, JOB;
  
์ถ๋ ฅ:
DNO                                                                              JOB                  COUNT(*) MAX(SALARY) SUM(SALARY) ROUND(AVG(SALARY)) GROUPING(DNO) GROUPING(JOB)
-------------------------------------------------------------------------------- ------------------ ---------- ----------- ----------- ------------------ ------------- -------------
10                                                                               CLERK                       1        1300        1300               1300             0             0
10                                                                               MANAGER                     1        2450        2450               2450             0             0
10                                                                               PRESIDENT                   1        5000        5000               5000             0             0
10                                                                               ์๊ณ                        3        5000        8750               2917             0             1
20                                                                               ANALYST                     2        3000        6000               3000             0             0
20                                                                               CLERK                       2        1100        1900                950             0             0
20                                                                               MANAGER                     1        2975        2975               2975             0             0
20                                                                               ์๊ณ                        5        3000       10875               2175             0             1
30                                                                               CLERK                       1         950         950                950             0             0
30                                                                               MANAGER                     1        2850        2850               2850             0             0
30                                                                               SALESMAN                    4        1600        5600               1400             0             0
30                                                                               ์๊ณ                        6        2850        9400               1567             0             1
ALL                                                                              ANALYST                     2        3000        6000               3000             1             0
ALL                                                                              CLERK                       4        1300        4150               1038             1             0
ALL                                                                              MANAGER                     3        2975        8275               2758             1             0
ALL                                                                              PRESIDENT                   1        5000        5000               5000             1             0
ALL                                                                              SALESMAN                    4        1600        5600               1400             1             0
์ด๊ณ                                                                                                        14        5000       29025               2073             1             1
```

</details>

<hr/>

### ๐ LISTAGG
โฝ ๊ทธ๋ฃน์ ๋ง๋ค๊ณ  ๊ทธ๋ฃน์ด ๋์ง ์์ ๋์ดํ๊ณ  ์ถ์ ์นผ๋ผ์ ๋ฐํํฉ๋๋ค.

<details>
<summary>๐์์  ์ฝ๋ ํ์ธ</summary><br>

```SQL
 -- LISTAGG ํจ์(์ค๋ผํด 11G ์ด์)
 SELECT DNO
      , LISTAGG(ENAME, ', ')
        WITHIN GROUP(ORDER BY SALARY DESC) AS ENAMES
   FROM EMPLOYEE
  GROUP BY DNO;
  
์ถ๋ ฅ:
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

### ๐ PIVOT
โฝ ๋ก์ฐ ๋จ์๋ฅผ ์นผ๋ผ ๋จ์๋ก ๋ณ๊ฒฝํด์ค๋๋ค.

<details>
<summary>๐์์  ์ฝ๋ ํ์ธ</summary><br>

```SQL
-- PIVOT ํจ์๋ฅผ ์ฌ์ฉํ์ฌ ์ง์ฑ๋ณ, ๋ถ์๋ณ ์ต๊ณ  ๊ธ์ฌ๋ฅผ 2์ฐจ์ ํ ํํ๋ก ์ถ๋ ฅํ๊ธฐ
 SELECT *
   FROM (SELECT DNO, JOB, SALARY
           FROM EMPLOYEE)
  PIVOT(MAX(SALARY)
        FOR DNO IN (10, 20, 30)
       )
  ORDER BY JOB;
  
์ถ๋ ฅ:
JOB                        10         20         30
------------------ ---------- ---------- ----------
ANALYST                             3000
CLERK                    1300       1100        950
MANAGER                  2450       2975       2850
PRESIDENT                5000
SALESMAN                                       1600
```
```SQL
 -- PIVOT ํจ์๋ฅผ ์ฌ์ฉํ์ฌ ๋ถ์๋ณ, ์ง์ฑ๋ณ ์ต๊ณ  ๊ธ์ฌ๋ฅผ 2 ์ฐจ์ ํ ํํ๋ก ์ถ๋ ฅ
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
 
์ถ๋ ฅ:
       DNO      CLERK   SALESMAN  PRESIDENT    MANAGER    ANALYST
---------- ---------- ---------- ---------- ---------- ----------
        10       1300                  5000       2450
        20       1100                             2975       3000
        30        950       1600                  2850
```

</details>

<hr/>

## โ ์ ๋ฆฌ ๋ฌธ์ 

<details>
<summary>๐์์  ์ฝ๋ ํ์ธ</summary><br>

```SQL
 -- ๊ฐ ๋ถ์์ ์์ฌ ์ฐ๋๋ณ ์ฌ์ ์, ์ต๊ณ  ๊ธ์ฌ, ๊ธ์ฌ ํฉ, ํ๊ท  ๊ธ์ฌ๋ฅผ ์ถ๋ ฅํ๊ณ 
 -- ๊ฐ ๋ถ์๋ณ ์๊ณ์ ์ด๊ณ๋ฅผ ์ถ๋ ฅํ์ธ์.
 SELECT DECODE(GROUPING(DNO), 1, DECODE(GROUPING(TO_CHAR(HIREDATE, 'YYYY')), 1, 'ALL'), DNO) AS DNO
      , DECODE(GROUPING(TO_CHAR(HIREDATE, 'YYYY')), 1
      , DECODE(GROUPING(DNO), 1, '์ด๊ณ', '์๊ณ'), TO_CHAR(HIREDATE, 'YYYY')) AS HIRE_YEAR
      , COUNT(*) AS CNT
      , MAX(SALARY) AS MAX_SAL
      , SUM(SALARY) AS SUM_SAL
      , TRUNC(AVG(SALARY)) AS AVG_SAL
   FROM EMPLOYEE
  GROUP BY ROLLUP(DNO, TO_CHAR(HIREDATE, 'YYYY'));
  
์ถ๋ ฅ:
DNO                                                                              HIRE_YEAR           CNT    MAX_SAL    SUM_SAL    AVG_SAL
-------------------------------------------------------------------------------- ------------ ---------- ---------- ---------- ----------
10                                                                               1981                  2       5000       7450       3725
10                                                                               1982                  1       1300       1300       1300
10                                                                               ์๊ณ                  3       5000       8750       2916
20                                                                               1980                  1        800        800        800
20                                                                               1981                  2       3000       5975       2987
20                                                                               1987                  2       3000       4100       2050
20                                                                               ์๊ณ                  5       3000      10875       2175
30                                                                               1981                  6       2850       9400       1566
30                                                                               ์๊ณ                  6       2850       9400       1566
ALL                                                                              ์ด๊ณ                 14       5000      29025       2073
```

</details>
