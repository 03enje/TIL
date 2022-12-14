## π μ‘°μΈ(JOIN)

β μ¬λ¬ νμ΄λΈμ μ μ₯λ λ°μ΄ν°λ₯Ό ν λ²μ μ‘°νν΄μΌ ν  νμκ° μλ κ²½μ° μ¬μ©ν©λλ€.

β WHERE μ μ λͺ¨νΈμ±μ λ°©μ§νκΈ° μν΄ μΉΌλΌλͺ μμ νμ΄λΈ λͺμ λͺμ  

β νμ΄λΈλͺμ΄ λλ¬΄ κΈ΄ κ²½μ°μ νμ΄λΈλͺμ λμ νλ λ³μΉ­ μ¬μ©  

β FROM μ μμ νμ΄λΈλͺμ λͺμνκ³  κ³΅λ°±μ λ λ€μ νμ΄λΈ λ³μΉ­μ μ§μ ν©λλ€.  

β νλμ SQL λͺλ Ήλ¬Έμμ νμ΄λΈλͺκ³Ό λ³λͺ νΌμ© λΆκ°λ₯, ν΄λΉ SQLλ¬Έ λ΄μμλ§ μ ν¨ν©λλ€.  

```SQL
 SELECT *
   FROM EMPLOYEE, DEPARTMENT
  WHERE EMPLOYEE.DNO = DEPARTMENT.DNO
  
 -- μ μλ SQL λͺλ Ήλ¬Έμ λλ±ν κ²°κ³Ό μΆλ ₯ -- 
 
 SELECT *
   FROM EMPLOYEE e, DEPARTMENT d
  WHERE e.DNO = d.DNO;
```

### π μΉ΄λ€μμ κ³±
β½ νΉλ³ν ν€μλ μμ΄ SELECT λ¬Έμ FROM μ μ λ κ° μ΄μμ νμ΄λΈμ μ½€λ§(,)λ‘ μ°κ²°νλ κΈ°μ 

<details>
<summary>πμμ  μ½λ νμΈ</summary>

```SQL
SELECT *
  FROM EMPLOYEE, DEPARTMENT;

-- μΆλ ₯ κ²°κ³Ό --
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

### π EQUI JOIN
β½ μ‘°μΈ λμ νμ΄λΈμμ κ³΅ν΅ μΉΌλΌμ '='(equal) λΉκ΅λ₯Ό ν΅ν΄ κ°μ κ°μ κ°μ§λ νμ μ°κ²°

#### π NATURAL JOIN

<details>
<summary>πμμΈν</summary><br>

π μ€λΌν΄μμ μλμ μΌλ‘ νμ΄λΈμ λͺ¨λ  μΉΌλΌμ λμμΌλ‘ μΌμΉνλ λ°μ΄ν° μ ν λ° μ΄λ¦μ κ°μ§ κ³΅ν΅ μΉΌλΌμ μ‘°μ¬ν ν μλμΌλ‘ μ‘°μΈ μν

```SQL
 SELECT E.ENO, E.ENAME, E.JOB, E.MANAGER, E.HIREDATE, E.SALARY, E.COMMISSION, DNO
     , D.DNAME, D.LOC
   FROM EMPLOYEE E NATURAL JOIN DEPARTMENT D;
```
```SQL
 -- κΈμ¬(SAL)κ° 2000 μ΄κ³ΌμΈ μ¬μλ€μ λΆμ μ λ³΄, μ¬μ μ λ³΄λ₯Ό μ€λ₯Έμͺ½κ³Ό κ°μ΄ μΆλ ₯ν΄ λ³΄μΈμ
 -- λ¨, NATURAL JOIN μ¬μ©
 SELECT DNO, D.DNAME, E.ENO, E.ENAME, E.SALARY AS SAL
   FROM EMPLOYEE E NATURAL JOIN DEPARTMENT D
  WHERE E.SALARY > 2000;

-- μΆλ ₯ κ²°κ³Ό --
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

#### π JOIN ~ USING

<details>
<summary>πμμΈν</summary><br>

π USING μ μ μ‘°μΈμ΄ λμμ΄ λλ μΉΌλΌμ μ§μ 

```SQL
 SELECT E.ENO, E.ENAME, E.JOB, E.MANAGER, E.HIREDATE, E.SALARY, E.COMMISSION, DNO
   , D.DNAME, D.LOC
   FROM EMPLOYEE E JOIN DEPARTMENT D USING(DNO);
```
```SQL
 -- λ€μ SQLλ¬Έμ JOINμ USING ν€μλλ₯Ό μ¬μ©ν λ±κ° μ‘°μΈμλλ€.
 -- μ‘°κ±΄1. μ¬μνμ΄λΈκ³Ό λΆμνμ΄λΈμ μ‘°μΈ μ‘°κ±΄μ λΆμ λ²νΈκ° κ°μ λμλλ€.
 -- μ‘°κ±΄2. κΈμ¬λ 3000 μ΄μμ΄λ©° μ§μμκ΄μ΄ λ°λμ μμ΄μΌ ν©λλ€.
 SELECT E.ENAME, E.MANAGER, DNO, D.DNAME, D.LOC, E.SALARY
   FROM EMPLOYEE E JOIN DEPARTMENT D USING(DNO)
  WHERE E.SALARY >= 3000
    AND E.MANAGER IS NOT NULL;

-- μΆλ ₯ κ²°κ³Ό --
ENAME                   MANAGER        DNO DNAME                        LOC                            SALARY
-------------------- ---------- ---------- ---------------------------- -------------------------- ----------
FORD                       7566         20 RESEARCH                     DALLAS                           3000
SCOTT                      7566         20 RESEARCH                     DALLAS                           3000
```
```SQL
 --SQL99 μ΄μ 
 -- κ° λΆμλ³ νκ·  κΈμ¬, μ΅λ κΈμ¬, μ΅μ κΈμ¬, μ¬μ μλ₯Ό μΆλ ₯ν΄ λ³΄μΈμ.
 -- λ¨, JOIN USING
 SELECT D.DNO, D.DNAME
      , TRUNC(AVG(E.SALARY)) AVG_SAL 
      , MAX(E.SALARY) MAX_SAL
      , MIN(E.SALARY) MIN_SAL
      , COUNT(E.ENO) CNT
   FROM EMPLOYEE E, DEPARTMENT D
  WHERE E.DNO = D.DNO
  GROUP BY D.DNO, D.DNAME;
  
 --SQL99 μ΄ν
 SELECT DNO, D.DNAME
      , TRUNC(AVG(E.SALARY)) AVG_SAL 
      , MAX(E.SALARY) MAX_SAL
      , MIN(E.SALARY) MIN_SAL
      , COUNT(E.ENO) CNT
   FROM EMPLOYEE E JOIN DEPARTMENT D USING(DNO)
  GROUP BY DNO, D.DNAME;
  
-- μΆλ ₯ κ²°κ³Ό --
       DNO DNAME                           AVG_SAL    MAX_SAL    MIN_SAL        CNT
---------- ---------------------------- ---------- ---------- ---------- ----------
        10 ACCOUNTING                         2916       5000       1300          3
        20 RESEARCH                           2175       3000        800          5
        30 SALES                              1566       2850        950          6
```

</details>

#### π JOIN ~ ON

<details>
<summary>πμμΈν</summary><br>

π μμμ μ‘°κ±΄μ μ§μ νκ±°λ μ‘°μΈν  μΉΌλΌμ μ§μ νλ €λ©΄ ON μ μ μ¬μ©
```SQL
 SELECT E.ENO, E.ENAME, E.JOB, E.MANAGER, E.HIREDATE, E.SALARY, E.COMMISSION
      , E.DNO, D.DNAME, D.LOC
   FROM EMPLOYEE E JOIN DEPARTMENT D ON(E.DNO = D.DNO)
  WHERE E.SALARY >= 3000;
```
```SQL
 --SQL99 μ΄μ 
 -- λͺ¨λ  λΆμ μ λ³΄μ μ¬μ μ λ³΄λ₯Ό μ€λ₯Έμͺ½κ³Ό κ°μ΄ λΆμ λ²νΈ, μ¬μ μ΄λ¦μμΌλ‘ μ λ ¬νμ¬ μΆλ ₯
 SELECT D.DNO, D.DNAME, E.ENO, E.ENAME, E.JOB, E.SALARY
   FROM EMPLOYEE E, DEPARTMENT D
  WHERE E.DNO(+) = D.DNO
  ORDER BY D.DNO, E.ENAME;
  
 --SQL99 μ΄ν
 SELECT D.DNO, D.DNAME, E.ENO, E.ENAME, E.JOB, E.SALARY
   FROM EMPLOYEE E JOIN DEPARTMENT D ON(E.DNO(+) = D.DNO)
  ORDER BY D.DNO, E.ENAME;
 
-- μΆλ ₯ κ²°κ³Ό --
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

### π NON EQUI JOIN
β½ WHERE μ μ '<', BETWEEN a AND bμ κ°μ΄ '=' μ‘°κ±΄μ΄ μλ μ°μ°μλ₯Ό μ¬μ©ν©λλ€

<details>
<summary>πμμ  μ½λ νμΈ</summary>

```SQL
 SELECT *
   FROM EMPLOYEE E, SALGRADE S
  WHERE E.SALARY BETWEEN S.LOSAL AND S.HISAL;
-- μΆλ ₯ κ²°κ³Ό--
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

### π SELF JOIN
β½ νλμ νμ΄λΈμ μλ μΉΌλΌλΌλ¦¬ μ°κ²°ν΄μΌ νλ μ‘°μΈμ΄ νμν κ²½μ° μ¬μ©

<details>
<summary>πμμ  μ½λ νμΈ</summary>

```SQL
 SELECT E.ENO, E.ENAME, E.MANAGER
      , M.ENO AS MRG_ENO
      , M.ENAME AS MGR_ENAME
  FROM EMPLOYEE E, EMPLOYEE M
 WHERE E.MANAGER = M.ENO;

-- μΆλ ₯ κ²°κ³Ό --
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
   
-- μΆλ ₯ κ²°κ³Ό --
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

### π OUTER JOIN
β½ EQUI JOINμμ μμΈ‘ μΉΌλΌ κ° μ€μ νλκ° NULLμ΄μ§λ§ μ‘°μΈ κ²°κ³Όλ‘ μΆλ ₯ν  νμκ° μλ κ²½μ° μ¬μ©

#### π (+) κΈ°νΈλ₯Ό μ¬μ©ν OUTER JOIN

<details>
<summary>πμμΈν</summary>

```SQL
 SELECT D.DNO, D.DNAME, E.ENO, E.ENAME, E.JOB, E.SALARY
   FROM EMPLOYEE E, DEPARTMENT D
  WHERE E.DNO(+) = D.DNO
  ORDER BY D.DNO, E.ENAME;
  
-- μΆλ ₯κ²°κ³Ό:
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

#### π ANSI OUTER JOIN(νμ€ μ‘°μΈ)

<details>
<summary>πμμΈν</summary><br>

π ANSI κ΅¬λ¬Έμμ OUTER JOINμ LEFT OUTER JOIN, RIGHT OUTER JOIN, FULL OUTER JOIN μΈ κ°μ§ νμμ μ‘°μΈμ μ κ³΅ν©λλ€.

```SQL
 SELECT D.DNO, D.DNAME, E.ENO, E.ENAME, E.JOB, E.SALARY
   FROM EMPLOYEE E RIGHT OUTER JOIN DEPARTMENT D ON(E.DNO = D.DNO)
  ORDER BY D.DNO, E.ENAME;
  
-- μΆλ ₯ κ²°κ³Ό --
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
 -- λͺ¨λ  λΆμ μ λ³΄, μ¬μ μ λ³΄, κΈμ¬ λ±κΈ μ λ³΄, κ° μ¬μμ μ§μ μκ΄μ μ λ³΄λ₯Ό
 -- λΆμ λ²νΈ, μ¬μ λ²νΈ μμλ‘ μ λ ¬
 --SQL99 μ΄μ 
 SELECT D.DNO, D.DNAME, E.ENO, E.ENAME, E.MANAGER, E.SALARY, E.DNO
      , S.LOSAL, S.HISAL, S.GRADE
      , M.ENO AS MGR_ENO
      , M.ENAME AS MGR_ENAME
   FROM EMPLOYEE E, EMPLOYEE M, DEPARTMENT D, SALGRADE S
  WHERE E.DNO(+) = D.DNO
        AND E.MANAGER = M.ENO(+)
        AND E.SALARY BETWEEN S.LOSAL(+) AND S.HISAL(+)
  ORDER BY D.DNO, E.ENO;
  
 --SQL99 μ΄ν
 SELECT D.DNO, D.DNAME, E.ENO, E.ENAME, E.MANAGER, E.SALARY, E.DNO
      , S.LOSAL, S.HISAL, S.GRADE
      , M.ENO AS MGR_ENO
      , M.ENAME AS MGR_ENAME
   FROM EMPLOYEE E RIGHT OUTER JOIN DEPARTMENT D ON(E.DNO = D.DNO)
        LEFT OUTER JOIN EMPLOYEE M ON(E.MANAGER = M.ENO)
        LEFT OUTER JOIN SALGRADE S ON(E.SALARY BETWEEN S.LOSAL AND S.HISAL)
  ORDER BY D.DNO, E.ENO;
-- μΆλ ₯ κ²°κ³Ό --
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

## β μ λ¦¬ λ¬Έμ 

<details>
<summary>πμμ  μ½λ νμΈ</summary>

 ```SQL
 -- 1. μ¬μμκ° 3λͺ μ΄μμΈ λΆμλͺκ³Ό μΈμμ μΆλ ₯ (group by, having)
 SELECT D.DNAME, COUNT(*)
   FROM EMPLOYEE E, DEPARTMENT D
  WHERE E.DNO = D.DNO
  GROUP BY D.DNAME
 HAVING COUNT(*) >= 3;
 ```
 ```SQL
 -- 2~3. μ¬μλ²νΈ, μ¬μμ΄λ¦, λΆμμ΄λ¦, λΆμλ²νΈλ₯Ό μΆλ ₯ (Natural Join, Join On, Join Using)
 SELECT E.ENO, E.ENAME, D.DNAME, DNO
   FROM EMPLOYEE E NATURAL JOIN DEPARTMENT D;
 SELECT E.ENO, E.ENAME, D.DNAME, DNO
   FROM EMPLOYEE E JOIN DEPARTMENT D USING(DNO);
 SELECT E.ENO, E.ENAME, D.DNAME, D.DNO
   FROM EMPLOYEE E JOIN DEPARTMENT D ON(E.DNO = D.DNO);
 ```
 ```SQL
 -- 4. λΆμκ° 30μ΄κ³ , κΈμ¬κ° 1500μ΄μμΈ μ¬μμ΄ μ΄λ¦, κΈμ¬, λΆμλͺ, λΆμλ²νΈλ₯Ό μΆλ ₯νμμ€.
 SELECT E.ENAME, E.SALARY, D.DNAME, D.DNO
   FROM EMPLOYEE E, DEPARTMENT D
  WHERE E.SALARY >= 1500
    AND E.DNO = D.DNO
    AND E.DNO = 30;
 ```
 ```SQL
 -- 5. ADAMS μ¬μμ΄ κ·Όλ¬΄νλ λΆμμ΄λ¦κ³Ό μ§μ­μ΄λ¦μ μΆλ ₯νμμ€.
 SELECT D.DNAME, D.LOC
   FROM EMPLOYEE E, DEPARTMENT D
  WHERE E.DNO = D.DNO
    AND E.ENAME = 'ADAMS';
 ```
 ```SQL
 -- 6. NEW YORK μ΄λ DALLAS μ§μ­μ κ·Όλ¬΄νλ μ¬μλ€μ μ¬μλ²νΈ, μ¬μμ΄λ¦μ μ¬μλ²νΈ μμΌλ‘ μΆλ ₯νμμ€.
 SELECT E.ENO, E.ENAME
   FROM EMPLOYEE E, DEPARTMENT D
  WHERE E.DNO = D.DNO
    AND D.LOC IN ('NEW YORK', 'DALLAS')
  ORDER BY E.ENAME;
 ```
 
 </details>