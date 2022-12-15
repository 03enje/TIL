# DML
> DML(데이터 조작어: Data Manipulation Language)은 테이블에 새로운 데이터를 삽입하거나 기존의 데이터를 수정, 삭제하기 위한 명령어의 집합

* 항상 모든 DML문을 실행하기 전 SELECT 문으로 데이터를 조회하여 알맞은 데이터를 변경할 것 인지 확인

## INSERT 문
> 테이블에 데이터를 입력하기 위한 명령어

```SQL
 INSERT INTO table_name(column_name, ... ) VALUES (column_value, ... );
```
* 한 번에 하나의 로우만 INTO 뒤에 명시한 테이블에 삽입
* 테이블명 뒤에 기술한 칼럼에 VALUES 절에서 지정한 칼럼 값을 순서대로 입력
* 삽입할 칼럼의 데이터 타입이 문자(CHAR, VARCHAR2)나 날짜(DATE)타입일 경우, 반드시 작은 따옴표('')를 함께 사용
```SQL
 --WHERE 0 = 1의 의미는 데이터를 제외한 구조(컬럼)만 복사, WHERE 1 <> 1도 같은 의미 즉, FALSE를 반환
 SELECT * FROM department 
  WHERE 0 = 1; 

 -- WHERE 1=1 사용 시 AND로 조건을 추가하여 간단하게 SQL 작성 가능
 -- 만약 없을 시 AND 조건을 WHERE로 가져와야 하기 때문에 불편함
 SELECT * FROM EMPLOYEE
  WHERE 1=1 AND DNO = 10 AND DNAME;
```
```SQL
 INSERT INTO DEPT_TEMP (DNO, DNAME, LOC)
 VALUES (50, 'DATABASE', 'SEOUL');
 
-- 출력 결과 --
       DNO DNAME                        LOC
---------- ---------------------------- --------------------------
        10 ACCOUNTING                   NEW YORK
        20 RESEARCH                     DALLAS
        30 SALES                        CHICAGO
        40 OPERATIONS                   BOSTON
        50 DATABASE                     SEOUL
        

1 행 이(가) 삽입되었습니다.

 INSERT INTO DEPT_TEMP 
                VALUES (60, 'NETWORK', 'BUSAN');
                
-- 출력 결과 --
       DNO DNAME                        LOC
---------- ---------------------------- --------------------------
        10 ACCOUNTING                   NEW YORK
        20 RESEARCH                     DALLAS
        30 SALES                        CHICAGO
        40 OPERATIONS                   BOSTON
        50 DATABASE                     SEOUL
        60 NETWORK                      BUSAN
```

### [NULL 값을 갖는 로우 삽입]
> 데이터를 입력하는 시점에서 해당 칼럼 값을 모르거나 확정되지 않았을 경우에는 칼럼의 값으로 NULL을 입력

* 암시적 방법은 입력 시 칼럼명 리스트에 해당 칼럼을 생략
```SQL
 -- 열 데이터를 넣지 않는 방식으로 NULL 데이터 입력 즉, DNAME을 NULL로 처리
 INSERT INTO DEPT_TEMP(DNO, LOC)
                VALUES( 90, 'INCHEON');
```
* 명시적 방법은 입력 시 VALUES 절에 명시적으로 NULL을 입력
```SQL
 -- NULL = ''
 INSERT INTO DEPT_TEMP(DNO, DNAME, LOC)
                VALUES(70, 'WEB', NULL);
                
 INSERT INTO DEPT_TEMP(DNO, DNAME, LOC)
                VALUES(80, 'MOBILE', '');
```

### [다른 테이블에서 데이터 복사]
* VALUES 절 대신 서브쿼리 사용
```SQL
 INSERT INTO table [(column1, column2, ... )]
 SUBQUERY;
```

### [에러를 갖는 경우]

#### |too many values| (칼럼 수 보다 값을 더 많이 추가)|
```SQL
 INSERT INTO DEPT_TEMP (DNO, DNAME, LOC)
                VALUES (60, 'NETWORK', 'BUSAN', 'ULSAN');
```

#### |not enough values|(칼럼 수 보다 값을 작게 추가)|
```SQL
 INSERT INTO DEPT_TEMP (DNO, DNAME, LOC)
 VALUES (50, 'DATABASE');
```

#### |invalid number|(칼럼의 형식에 맞지 않는 값을 추가)
```SQL
 INSERT INTO DEPT_TEMP (DNO, DNAME, LOC)
                VALUES ('WRONG', 'NETWORK', 'BUSAN');
```

#### |value larger than specified precision allowed for this column| (칼럼의 자릿수를 초과한 값을 추가)
```SQL
 INSERT INTO DEPT_TEMP (DNO, DNAME, LOC)
                VALUES (600, 'NETWORK', 'BUSAN');
```

#### |date format picture ends before converting entire input string| (데이터 형식을 틀리게 입력)
```SQL
 -- 날짜 형식은 YYYY/MM/DD 순
 -- 만약, DD/MM/YYYY 순을 원한다면 다음과 같이 TO_DATE 사용
 TO_DATE('05/01/2001', 'DD/MM/YYYY')
```


## UPDATE 문
> 테이블에 저장된 데이터를 수정하기 위한 명령어
```SQL
 UPDATE table_name
 SET column_name1 = value1, column_name2 = value2, ...
 WHERE conditions;
```
```SQL
 -- EMP_TABLE 테이블의 사원들 중에서
 -- 급여가 2500 이하인 사원만 추가 수당(COMMISSION)을 50으로 수정
 -- 항상 SELECT 문으로 먼저 데이터를 확인
 SELECT ENAME, COMMISSION, SALARY
   FROM EMP_TEMP
  WHERE SALARY <= 2500;
  
 UPDATE EMP_TEMP
    SET COMMISSION = 50
  WHERE SALARY <= 2500;
  
-- 출력 결과 --
ENAME      COMMISSION     SALARY
---------- ---------- ----------
SMITH              50        800
ADAMS              50       1100
JAMES              50        950
```
### [다른 테이블을 기반으로 데이터 수정]
* SET 절에서 서브쿼리 사용
```SQL
 UPDATE DEPT_TEMP2
    SET (DNAME, LOC) = (SELECT DNAME, LOC
                          FROM DEPARTMENT
                         WHERE DNO = 40)
  WHERE DNO = 40;

-- 출력 결과 --
       DNO DNAME          LOC          
---------- -------------- -------------
        10 ACCOUNTING     NEW YORK     
        20 RESEARCH       DALLAS       
        30 SALES          CHICAGO      
        40 OPERATIONS     BOSTON       
```
* WHERE 절에서 서브쿼리 사용
```SQL
UPDATE DEPT_TEMP2
    SET LOC = 'SEOUL'
  WHERE DNO = (SELECT DNO 
                  FROM DEPT_TEMP2 
                 WHERE DNAME = 'OPERATIONS');
```
## DELETE 문
> 테이블에 저장된 데이터를 삭제하기 위한 명령어
```SQL
 DELETE [FROM] table_name
 WHERE conditions;
```
```SQL
 -- DELETE, UPDATE는 하기 전 항상 백업 필수
 SELECT * FROM EMP_TEMP2 WHERE JOB = 'MANAGER';
 /*
 7566	JONES	MANAGER	7839	1981-04-02	2975		20
 7698	BLAKE	MANAGER	7839	1981-05-01	2850		30
 7782	CLARK	MANAGER	7839	1981-06-09	2450		10 
 */
 DELETE FROM EMP_TEMP2 WHERE JOB = 'MANAGER';
```
### [다른 테이블을 기반으로 로우 삭제]
* DELETE 문에서 서브쿼리 사용
* WHERE 절에서 서브쿼리 사용
```SQL
 -- WHERE 절에 서브쿼리를 사용하여 데이터 일부만 삭제
 SELECT E.*
   FROM EMP_TEMP2 E, SALGRADE S
  WHERE E.SALARY BETWEEN S.LOSAL AND S.HISAL
    AND S.GRADE = 3
    AND DNO = 30;
    
 SELECT *
   FROM EMP_TEMP2
  WHERE ENO IN (SELECT E.ENO
                   FROM EMP_TEMP2 E, SALGRADE S
                  WHERE E.SALARY BETWEEN S.LOSAL AND S.HISAL
                    AND S.GRADE = 3
                    AND DNO = 30);
-- 데이터 백업
/*
7499	ALLEN	SALESMAN	7698	1981-02-20	1600	300	30
7844 TURNER	SALESMAN	7698	1981-09-08	1500	0	30
*/

 DELETE
   FROM EMP_TEMP2
  WHERE ENO IN (SELECT E.ENO
                   FROM EMP_TEMP2 E, SALGRADE S
                  WHERE E.SALARY BETWEEN S.LOSAL AND S.HISAL
                    AND S.GRADE = 3
                    AND DNO = 30);
```