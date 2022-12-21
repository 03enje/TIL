# 기본 함수

## 문자 함수
### [대소문자 변환 함수]
|구분|설명|
|---|---|
|LOWER|소문자 변환|
|UPPER|대문자 변환|
|INITCAP|첫 글자만 대문자|

### [문자 길이 반환 함수]
|구분|설명|
|---|---|
|LENGTH|문자의 길이 반환(한글 1BYTE)|
|LENGTHB|문자의 길이 반환(한글 3BYTE)|

#### * 반환 값이 3BYTE인 이유는?
> 오라클은 기본값으로 UTF-8(3BYTE)를 사용하기 때문입니다.

```SQL
SELECT *
  FROM nls_database_parameters
 WHERE parameter = 'NLS_CHARACTERSET';
 
출력:
PARAMETER                      VALUE                                   
------------------------------ ----------------------------------------
NLS_CHARACTERSET               AL32UTF8                                

-- AL32UTF8(한글 바이트) : 3BYTE
-- KO16KSC5601(완성형 한글) : 2BYTE
-- KO16MSWIN949(조합형 한글) : 2BYTE
```

### [문자 조작 함수]
|구분|설명|
|----|----|
|CONCAT|문자의 값 연결|
|SUBSTR|문자를 잘라 추출(1BYTE)|
|SUBSTRB|문자를 잘라 추출(3BYTE)|
|INSTR|특정 문자의 위치 값 반환(1BYTE)|
|INTSTRB|특정 문자의 위치 값 반환(3BYTE)|
|LPAD, RPAD|입력 받은 문자열과 기호를 정렬하여 특정 길이의 문자열 반환|
|TRIM|잘라내고 남은 문자 표시|

#### |CONCAT|
```SQL
SELECT 'ORACLE', 'MANIA', CONCAT('Oracle', 'mania') 
  FROM dual;

출력:
'ORACLE'     'MANIA'    CONCAT('ORACLE','MANIA)
------------ ---------- ----------------------
ORACLE       MANIA      Oraclemania
```

#### |SUBSTR|, |SUBSTRB|
```SQL
SELECT SUBSTR('오라클매니아', 3, 4), SUBSTRB('오라클매니아', 3, 4)
  FROM dual;

출력:
SUBSTR('오라클매니아',3, SUBSTRB('오라클매니아', 3, 4)
------------------------ --------
클매니아                  라
```

#### |INSTR|
```SQL
SELECT INSTR('Oracle mania', 'a')
  FROM dual;

출력:
INSTR('ORACLEMANIA','A')
------------------------
                       3
```

#### |LPAD|, |RPAD|
```SQL
SELECT LPAD(SALARY, 10, '*')
  FROM employee;

출력:
LPAD(SALARY,10,'*')
--------------------------------------------------------------------------------
*******800
******1600
******1250
...
```
```SQL
SELECT RPAD(SALARY, 10, '*')
  FROM employee;

출력:
RPAD(SALARY,10,'*')
--------------------------------------------------------------------------------
800*******
1600******
1250******
...
```

#### |TRIM|
```SQL
SELECT 'Oracle mania', TRIM('O' FROM 'Oracle mania')
  FROM dual;

출력:
'ORACLEMANIA'            TRIM('O'FROM'ORACLEMAN
------------------------ ----------------------
Oracle mania             racle mania
```

### [정리]
```SQL
/*
 * ENO 열에는 EMPLOYEE 테이블에서 사원 이름이 다섯 글자 이상 여섯 글자 미만인 사원 정보를 출력,
 * MASKING_ENO 열에는 사원 번호앞 두 자리 외 뒷자리를 * 기호로 출력,
 * 그리고 MASKING_ENAME 열에는 사원 이름의 첫 글자만 보여 주고 나머지 글자 수 만큼 * 출력합니다.
 */

SELECT eno
     , RPAD(SUBSTR(eno, 1, 2), 4, '*') AS masking_eno
     , ename
     , RPAD(SUBSTR(ename, 1, 1), 5, '*') AS masking_ename
  FROM employee
 WHERE LENGTH(ename) >= 5 AND LENGTH(ename) < 6;
 
출력:
       ENO MASKING_ENO                      ENAME                MASKING_ENAME
---------- -------------------------------- -------------------- ----------------------------------------
      7369 73**                             SMITH                S****
      7499 74**                             ALLEN                A****
      7566 75**                             JONES                J****
      7698 76**                             BLAKE                B****
...
```

- - -

## 숫자 함수
|구분|설명|
|----|----|
|ROUND|특정 자릿수에서 반올림|
|TRUNC|특정 자릿수에서 버림|
|MOD|입력 받을 수를 나눈 나머지 값 반환|

### [ROUND], [TRUNC]
```SQL
SELECT salary / 21 / 8 AS 시급
     , ROUND(salary / 21 / 8, 1)
     , salary / 21 AS 일급
     , TRUNC(salary / 21, 2)
  FROM employee;
  
출력:
        시급 ROUND(salary/21/8,1)       일급 TRUNC(salary/21,2)
---------- -------------------- ---------- ------------------
4.76190476                  4.8 38.0952381              38.09
9.52380952                  9.5 76.1904762              76.19
7.44047619                  7.4 59.5238095              59.52
```

### [MOD]
```SQL
SELECT MOD(15, 6)
     , MOD(10, 2)
     , MOD(11,2)
  FROM dual;
  
출력:
 MOD(15,6)  MOD(10,2)  MOD(11,2)
---------- ---------- ----------
         3          0          1
```

### [CEIL], [FLOOR]
> CEIL은 수를 올림, FLOOR는 수를 내림 하는 함수
```SQL
SELECT CEIL(3.14), FLOOR(3.14)
     , CEIL(-3.14), FLOOR(-3.14)  
  FROM dual;
 
출력:
CEIL(3.14) FLOOR(3.14) CEIL(-3.14) FLOOR(-3.14)
---------- ----------- ----------- ------------
         4           3          -3           -4
```

- - -

## 날짜 함수
|구분|설명|
|----|----|
|SYSDATE|시스템에 저장된 현재 날짜 반환|
|MONTHS_BETWEEN|두 날짜 사이가 몇 개월인지를 반환|
|ADD_MONTHS|특정 날짜에 개월 수를 더함|
|NEXT_DAY|특정 날짜에서 최초로 도래하는 인자로 받은 요일의 날짜 반환|
|LAST_DAY|해당 달의 마지막 날짜 반환|
|ROUND|인자로 받은 날짜를 특정 기준으로 반올림|
|TRUNC|인자로 받은 날짜를 특정 기준으로 버림|

### [SYSDATE]
```SQL
SELECT sysdate FROM dual;

출력:
sysdate
--------
22/11/30
```
> 환경설정 -> 데이터베이스 -> NLS -> 날짜 형식에 따라 출력이 달라집니다.(기본 사용 형식: YYYY-MM-DD)

### [ADD_MONTHS]
```SQL
SELECT sysdate
     , ADD_MONTHS(sysdate, 3) AS "3개월 후"
  FROM daul;

출력:
sysdate  3개월 후
-------- --------
22/11/30 23/02/28
```

### [정리]
```SQL

/*
 * EMP 테이블에서 사원들의 일 평균 근무일 수는 21.5일, 하루 근무 시간을 8시간으로 보았을 때
 * 사원들의 하루 급여(DAY_PAY)와 시급(TIME_PAY)를 계산하여 결과 출력합니다.
 * 단, 하루 급여는 소수점 세 번째 자리에서 버리고, 시급은 두 번째 소수점에서 반올림

SELECT eno, ename, salary
     , TRUNC((salary / 21.5), 2) AS day_pay
     , ROUND((salary / 21.5 / 8), 1) AS time_pay
  FROM employee;
  
출력:
       eno ename                    salary    day_pay   time_pay
---------- -------------------- ---------- ---------- ----------
      7369 SMITH                       800       37.2        4.7
      7499 ALLEN                      1600      74.41        9.3
      7521 WARD                       1250      58.13        7.3
      7566 JONES                      2975     138.37       17.3
      7654 MARTIN                     1250      58.13        7.3
      7698 BLAKE                      2850     132.55       16.6
```

- - -

## 형 변환 함수
> 오라클에서 데이터형을 변환해야 하는 경우에는 TO_NUMBER, TO_CHAR, TO_DATE를 사용합니다.

|구분|설명|
|----|----|
|TO_CHAR|날짜형 혹은 숫자형을 문자형으로 변환|
|TO_DATE|문자형을 날짜형으로 변환|
|TO_NUMBER|문자형을 숫자형으로 변환|

### [TO_CHAR]
```SQL
-- TO_CHAR는 문자 포맷을 지정해서 출력하고 싶을때 주로 사용
SELECT TO_CHAR(SYSDATE, 'YYYY/MM/DD HH24:MI:SS') FROM dual;

출력:
TO_CHAR(SYSDATE,'YYYY/MM/DDHH24:MI:SS'
--------------------------------------
2022/11/30 14:53:39
```

### [묵시적 형 변환]
* 숫자열에 문자를 더하여 출력하기
```SQL
SELECT ENAME, ENO, ENO + '500'
  FROM EMPLOYEE
 WHERE ENAME = 'SCOTT';
 
출력:
ENAME                       ENO  ENO+'500'
-------------------- ---------- ----------
SCOTT                      7788       8288
```

* 문자열과 숫자를 더하여 출력하기(숫자로 인식 가능한 문자만 가능)
```SQL
SELECT '500' + ENO, ENO
  FROM EMPLOYEE
 WHERE ENAME = 'SCOTT';
 
출력:
  '500'+ENO        ENO
---------- ----------
      8288       7788
```

- - -

## 일반 함수

### [NVL]
> NULL, ? 은 ∞의 의미이기 때문에 연산, 할당, 비교가 불가능합니다. 따라서 NULL을 0또는 다른 값으로 변환하기 위해서 사용하는 함수입니다. 
```SQL
SELECT ename, salary, commission
     , NVL(commission, 0)
     , salary*12+NVL(commission, 0)
  FROM employee 
 ORDER BY job;

출력:
ENAME                    SALARY COMMISSION NVL(COMMISSION,0) SALARY*12+NVL(COMMISSION,0)
-------------------- ---------- ---------- ----------------- ---------------------------
SCOTT                      3000                            0                       36000
FORD                       3000                            0                       36000
MILLER                     1300                            0                       15600
...
```

### [NVL2(expr1, expr2, expr3)]
> expr1을 검사하여 그 결과가 널이 아니면 expr2를 반환하고 널이면 expr3을 반환합니다.

```SQL
SELECT eno, ename, commission
     , NVL2(commission, '존재', '부재')
  FROM employee;
  
출력:
       ENO ENAME                COMMISSION NVL2(COMMISS
---------- -------------------- ---------- ------------
      7369 SMITH                           부재
      7499 ALLEN                       300 존재
      7521 WARD                        500 존재
      7566 JONES                           부재
...
```

### [NVLIF(expr1, expr2)]
> 두 표현식을 비교하여 동일한 경우에는 널을 반환하고 동일하지 않으면 첫 번째 표현식을 반환합니다.

```SQL
SELECT NULLIF('A', 'A'), NULLIF('A', 'B') FROM dual;

출력:
NU NU
-- --
   A
```

### [DECODE]
> [DECODE(표현식, 조건1, 결과1, 조건2, 결과2, 조건3, 결과3, 기본결과n)]

```SQL
SELECT eno, ename, job, salary
     , DECODE(job,
               'MANAGE', salary*1.1,
               'SALESMAN', salary*1.05,
               'ANALYST', salary,
               salary*1.03) AS upsalary
  FROM employee;

출력:
       eno ename                job                    salary   upsalary
---------- -------------------- ------------------ ---------- ----------
      7369 SMITH                CLERK                     800        824
      7499 ALLEN                SALESMAN                 1600       1680
      7521 WARD                 SALESMAN                 1250     1312.5
      7566 JONES                MANAGER                  2975    3064.25
      7654 MARTIN               SALESMAN                 1250     1312.5
```

### [CASE]
> [CASE 표현식 WHEN 조건1 THEN 결과1 WHEN 조건2 THEN 결과2 WHEN 조건3 THEN 결과3 ELSE 결과n END]

```SQL
SELECT eno, ename, job, salary
     , CASE job
            WHEN 'MANAGER' THEN salary*1.1
            WHEN 'SALESMAN' THEN salary*1.05
            WHEN 'ANALYST' THEN salary
            ELSE salary*1.03
        END AS upsalary
  FROM employee;
  
출력:
       eno ename                job                    salary   upsalary
---------- -------------------- ------------------ ---------- ----------
      7369 SMITH                CLERK                     800        824
      7499 ALLEN                SALESMAN                 1600       1680
      7521 WARD                 SALESMAN                 1250     1312.5
      7566 JONES                MANAGER                  2975     3272.5
      7654 MARTIN               SALESMAN                 1250     1312.5
```
```SQL
SELECT eno, ename, commission
     , CASE
            WHEN commission IS NULL THEN '해당사항 없음'
            WHEN commission = 0 THEN '수당없음'
            WHEN commission > 0 THEN '수당 : ' || COMMISSION
        END AS comm_text
  FROM employee;

출력:
       ENO ENAME                COMMISSION COMM_TEXT
---------- -------------------- ---------- --------------------------------------------------------------------------------------------------
      7369 SMITH                           해당사항 없음
      7499 ALLEN                       300 수당 : 300
      7566 JONES                           해당사항 없음
      7654 MARTIN                     1400 수당 : 1400
      7698 BLAKE                           해당사항 없음
      7844 TURNER                        0 수당없음
```

### [정리]
```SQL
/*
 * EMP 테이블에서 사원들은 입사일을 기준으로 3개월이 지난 후 첫 월요일에 정직원
 * 사원들이 정직원이 되는 날짜(R_JOB)를 'YYYY-MM-DD'형식으로 출력합니다.
 * 단, 추가 수당(COMMISSION)이 없는 사원의 추가 수당은 N/A로 출력
 */
SELECT ENO, ENAME, HIREDATE, NVL(TO_CHAR(COMMISSION), 'N/A') AS "COMM"
     , TO_CHAR(NEXT_DAY(ADD_MONTHS(HIREDATE, 3), '월요일'), 'YYYY-MM-DD') AS "R_JOB"
  FROM EMPLOYEE;
  
출력:
      ENO ENAME                HIREDATE COMM                                                                             R_JOB
---------- -------------------- -------- -------------------------------------------------------------------------------- --------------------
      7369 SMITH                80/12/17 N/A                                                                              1981-03-23
      7499 ALLEN                81/02/20 300                                                                              1981-05-25
      7521 WARD                 81/02/22 500                                                                              1981-05-25
      7566 JONES                81/04/02 N/A                                                                              1981-07-06
      7654 MARTIN               81/09/28 1400                                                                             1982-01-04
```

```SQL
SELECT ENO, ENAME, MANAGER
     , CASE 
            WHEN MANAGER IS NULL THEN '0000'
            WHEN TO_CHAR(SUBSTR(MANAGER, 1, 2)) = '75' THEN '5555'
            WHEN TO_CHAR(SUBSTR(MANAGER, 1, 2)) = '76' THEN '6666'
            WHEN TO_CHAR(SUBSTR(MANAGER, 1, 2)) = '77' THEN '7777'
            WHEN TO_CHAR(SUBSTR(MANAGER, 1, 2)) = '78' THEN '8888'
            ELSE TO_CHAR(MANAGER)
       END AS CHG_MANAGER
FROM EMPLOYEE;

출력:
       ENO ENAME                   MANAGER CHG_MANAGER
---------- -------------------- ---------- --------------------------------------------------------------------------------
      7369 SMITH                      7902 7902
      7499 ALLEN                      7698 6666
      7521 WARD                       7698 6666
      7566 JONES                      7839 8888
      7654 MARTIN                     7698 6666
      7698 BLAKE                      7839 8888
      7782 CLARK                      7839 8888
      7788 SCOTT                      7566 5555
      7839 KING                            0000
      7844 TURNER                     7698 6666
      7876 ADAMS                      7788 7777
      7900 JAMES                      7698 6666
      7902 FORD                       7566 5555
      7934 MILLER                     7782 7777
```
- - -