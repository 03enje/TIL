# PL/SQL
> PL/SQL(Oracle's Procedural Language extension to SQL)은 오라클에서 지원하는 프로그래밍 언어의 특성을 수용하여 SQL에서는 사용할 수 없는 절차적 프로그래밍 기능을 가지고 있어 SQL의 단점을 보완합니다.

|구분|설명|필수여부|
|---|---|---|
|DECLARE(선언부))|모든 변수나 상수를 선언|옵션|
|BEGIN(실행부)|제어문, 반복문, 함수 정의 등 로직을 기술|필수|
|EXCEPTION(예외처리부)|예외 처리를 기술|옵션|

## 시스템 입력 
> ACCEPT value PROMPT '값 입력';

```SQL
ACCEPT num1 PROMPT '값을 입력해주세요';
DECLARE
  V_NUM NUMBER := &num1;
BEGIN
  DBMS_OUTPUT.PUT_LINE('값은 : ' || V_NUM);
END;
/
```

## 시스템 출력
> SET SERVEROUTPUT ON;  
> DBMS_OUTPUT.PUT_LINE에서 입력을 받아 입력값들을 콘솔에 출력합니다.

```SQL
SQL>
SET SERVEROUTPUT ON;

BEGIN
  DBMS_OUTPUT.PUT_LINE('Hello, PL/SQL!');
END;

SQL> /

-- OUTPUT --
Hello, PL/SQL!
```

## DECLARE(선언부)

* 변수 선언
``` SQL
SQL>
DECLARE
  -- 변수 선언
  -- V_TAX CONSTANT NUMBER(1) := 3;          -- 상수
  -- V_DEPTNO NUMBER(2) DEFAULT 10;          -- 기본값
  -- V_DEPTNO NUMBER(2) NOT NULL := 10;      -- NOT NULL
  -- V_DEPTNO NUMBER(2) NOT NULL DEFAULT 10; -- NOT NULL, 기본값
  V_DEPTNO DEPARTMENT.DNO%TYPE  := 50;       -- 참조 변수 타입
  
BEGIN  
  -- DBMS_OUTPUT.PUT_LINE('V_TAX : ' || V_TAX);
  DBMS_OUTPUT.PUT_LINE('V_DEPTNO : ' || V_DEPTNO);
END;

SQL> /
-- OUTPUT --
V_TAX : 3
```

* 테이블 데이터 가져오기
```SQL
SQL>
DECLARE
  -- 테이블 ROW값 참조
  V_DEPT_ROW DEPARTMENT%ROWTYPE;
BEGIN  
  SELECT    DNO, DNAME, LOC
  INTO       V_DEPT_ROW
  FROM     DEPARTMENT
  WHERE    DNO = 40;
  DBMS_OUTPUT.PUT_LINE('DNO : ' || V_DEPT_ROW.DNO);
  DBMS_OUTPUT.PUT_LINE('DNAME : ' || V_DEPT_ROW.DNAME);
  DBMS_OUTPUT.PUT_LINE('LOC : ' || V_DEPT_ROW.LOC);
END;

SQL> /

-- OUTPUT --
DNO : 40
DNAME : OPERATIONS
LOC : BOSTON
```
```SQL
-- 직원번호가 7900 인 직원정보를 ROWTYPE변수를 활용하여 데이터를 출력 해보세요
DECLARE
  V_ROW   EMPLOYEE%ROWTYPE;
/* 
   칼럼을 개별적으로 사용할 때
 * V_NO    EMPLOYEE.ENO%TYPE;
 * V_NAME  EMPLOYEE.ENAME%TYPE;
 * V_SAL   EMPLOYEE.SALARY%TYPE;
 */
BEGIN
  SELECT ENO, ENAME, SALARY
    INTO V_ROW.ENO, V_ROW.ENAME, V_ROW.SALARY
    -- INTO V_NO, V_NAME, V_SAL -- 칼럼을 개별적으로 사용할 때
    FROM EMPLOYEE
   WHERE ENO = 7900;
   
  DBMS_OUTPUT.PUT_LINE('직원정보: ' || V_ROW.ENO || ' ' ||
                          V_ROW.ENAME || ' ' || V_ROW.SALARY);
END;
/

-- OUTPUT --
직원정보: 7900 JAMES 950
```
## BEGIN(실행부)

* IF 문
```SQL
DECLARE
  V_NUMBER NUMBER := 14;
BEGIN
  -- IF 문을 사용하여 값 출력
  IF MOD(V_NUMBER, 2) = 1 THEN
    DBMS_OUTPUT.PUT_LINE('V_NUMBER는 홀수입니다.');
  ELSE
    DBMS_OUTPUT.PUT_LINE('V_NUMBER는 짝수입니다.');
  END IF;
END;
/

-- OUTPUT --
V_NUMBER는 짝수입니다.
```
* IF ~ ELSIF 문
```SQL
DECLARE
  V_SCORE NUMBER := 87;
BEGIN  
    -- IF ~ ELSIF 문을 사용하여 값 출력
  IF V_SCORE >= 90 THEN
    DBMS_OUTPUT.PUT_LINE('A학점');
  ELSIF V_SCORE >= 80 THEN
    DBMS_OUTPUT.PUT_LINE('B학점');
  ELSIF V_SCORE >= 70 THEN
    DBMS_OUTPUT.PUT_LINE('C학점');
  ELSIF V_SCORE >= 60 THEN
    DBMS_OUTPUT.PUT_LINE('D학점');
  ELSE
    DBMS_OUTPUT.PUT_LINE('F학점');
  END IF;
END;
/

-- OUTPUT --
B학점
```
```SQL
/*
 * 7369 사원의 급여가 10000 이상이면 '상'을
 * 5000 이상이면 '중'을 그 이하면 '하'를 출력하시오.
 * 단, '상', '중', '하'의 변수는 V_LEVEL 이며
 * DBMS_OUTPUT.PUT_LINE(V_EMPNO || '번 사원의 급여' || V_SALARY || '는 ' || V_LEVEL)
 */ 
 
DECLARE
  V_EMPNO  EMPLOYEE.ENO%TYPE := 7369;
  V_SALARY EMPLOYEE.SALARY%TYPE;
  V_LEVEL  VARCHAR2(4) := 'NULL'; -- 상, 중, 하
BEGIN
  SELECT SALARY
    INTO V_SALARY
    FROM EMPLOYEE
   WHERE EMPLOYEE.ENO = V_EMPNO;
    
  IF V_SALARY >= 10000 THEN
    V_LEVEL := '상';
  ELSIF V_SALARY >= 5000 THEN
    V_LEVEL := '중';
  ELSE
    V_LEVEL := '하';
  END IF;
  
  DBMS_OUTPUT.PUT_LINE(V_EMPNO || '번 사원의 급여 ' || V_SALARY || '$는 ' ||
                         '급여 레벨 ' || V_LEVEL || ' 등급입니다.');
END;
/

-- OUTPUT --
7369번 사원의 급여 800$는 급여 레벨 하 등급입니다.
```

* CASE 문
```SQL
DECLARE
  V_SCORE NUMBER := 87;
BEGIN  
  -- CASE 문을 사용하여 값 출력
  CASE TRUNC(V_SCORE/10)
      WHEN 10 THEN
        DBMS_OUTPUT.PUT_LINE('A학점');
      WHEN 9 THEN
        DBMS_OUTPUT.PUT_LINE('A학점');
      WHEN 8 THEN
        DBMS_OUTPUT.PUT_LINE('B학점');
      WHEN 7 THEN
        DBMS_OUTPUT.PUT_LINE('C학점');
      WHEN 6 THEN
        DBMS_OUTPUT.PUT_LINE('D학점');
      ELSE 
        DBMS_OUTPUT.PUT_LINE('F학점');
        
      -- 다음과 같이 사용할 수도 있습니다.
      /*
      BEGIN  
        CASE
            WHEN V_SCORE >= 90 THEN
              DBMS_OUTPUT.PUT_LINE('A학점');
            WHEN V_SCORE >= 80 THEN
              DBMS_OUTPUT.PUT_LINE('B학점');
            ELSE 
              DBMS_OUTPUT.PUT_LINE('F학점');
        END CASE;
      END
      */
      
  END CASE;
END;
/

-- OUTPUT --
C학점
```
```SQL
/* DEPT 테이블의 DEPTNO와 자료형이 같은 변수 V_DEPTNO를 선언합니다. 그리고 V_DEPTNO 변수 값에
 * 10, 20, 30, 40을 대입했을 때 다음과 같이 부서 이름을 출력하는 프로그램을 작성
 * 단, 부서 번호가 해당되지 않으면 N/A로 출력합니다.
 */
ACCEPT DNO PROMPT '부서번호?';
DECLARE
  -- [변수 선언 및 값 대입]
  V_DEPTNO DEPARTMENT.DNO%TYPE := &DNO; -- 초기화값
BEGIN
  -- [PL/SQL 작성]
  CASE V_DEPTNO
    WHEN 10 THEN
      DBMS_OUTPUT.PUT_LINE('DNAME : ACCOUNTING');
    WHEN 20 THEN
      DBMS_OUTPUT.PUT_LINE('DNAME : RESEARCH');
    WHEN 30 THEN
      DBMS_OUTPUT.PUT_LINE('DNAME : SALES');
    WHEN 40 THEN
      DBMS_OUTPUT.PUT_LINE('DNAME : OPERATIONS');
    ELSE
      DBMS_OUTPUT.PUT_LINE('N/A');
  END CASE;
END;
/
```

* LOOP 문
```SQL
DECLARE
  V_NUM NUMBER := 0;
BEGIN  
  -- LOOP 문을 사용하여 값 출력
  LOOP
       DBMS_OUTPUT.PUT_LINE('현재 V_NUM : ' || V_NUM);
       V_NUM := V_NUM + 1;
         EXIT WHEN V_NUM > 4;
       -- IF 문은 또 다른 루프 탈출방법
       IF V_NUM > 4 THEN
         EXIT;
       END IF;
  END LOOP;
END;
/

-- OUTPUT --
현재 V_NUM : 0
현재 V_NUM : 1
현재 V_NUM : 2
현재 V_NUM : 3
현재 V_NUM : 4
```
```SQL
-- BASIC LOOP로 1부터 숫자 홀수 10개 출력하기
DECLARE
  V_NUM NUMBER := 1;
  V_COUNT NUMBER := 1;
BEGIN
  LOOP
    EXIT WHEN V_COUNT > 10;
    DBMS_OUTPUT.PUT_LINE(V_NUM);
    V_NUM := V_NUM + 2;
    V_COUNT := V_COUNT + 1;
  END LOOP;
END;
/

-- OUTPUT --
1
3
5
7
9
11
13
15
17
19
```
* WHILE 문
```SQL
DECLARE
  V_NUM NUMBER := 0;
BEGIN  
  -- WHILE 문을 사용하여 값 출력
  WHILE V_NUM < 5 
    LOOP
         DBMS_OUTPUT.PUT_LINE('현재 V_NUM : ' || V_NUM);
         V_NUM := V_NUM + 1;
    END LOOP;
END;
/

-- OUTPUT --
현재 V_NUM : 0
현재 V_NUM : 1
현재 V_NUM : 2
현재 V_NUM : 3
현재 V_NUM : 4
```
```SQL
-- WHILE LOOP로 1부터 숫자 홀수 10개 출력하기
DECLARE
  V_NUM NUMBER := 1;
  V_COUNT NUMBER := 1;
BEGIN
  WHILE V_COUNT <= 10 LOOP
    DBMS_OUTPUT.PUT_LINE(V_NUM);
    V_NUM := V_NUM + 2;
    V_COUNT := V_COUNT + 1;
  END LOOP;
END;
/
```
* FOR 문
```SQL
DECLARE
  V_NUM NUMBER := 0;
BEGIN 
  -- FOR 문을 사용하여 값 출력
  FOR i IN 0..4 
    LOOP
      DBMS_OUTPUT.PUT_LINE('현재 i의 값 : ' || i);
    END LOOP;
END;
/

-- OUTPUT --
현재 i의 값 : 0
현재 i의 값 : 1
현재 i의 값 : 2
현재 i의 값 : 3
현재 i의 값 : 4
```

* CONTINUE 문
```SQL
BEGIN
  -- 홀수면 남은 명령문을 수행 않고 다음 반복주기로 스킵
  FOR i IN 0..4 LOOP
    CONTINUE WHEN MOD(i, 2) = 1;
    DBMS_OUTPUT.PUT_LINE('현재 i의 값 : ' || i);
  END LOOP;
END;
/

-- OUTPUT --
현재 i의 값 : 0
현재 i의 값 : 2
현재 i의 값 : 4
```