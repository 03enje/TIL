## 레코드
> 자료형이 다른 여러 데이터를 저장하는 변수
```SQL
/*
 * 레코드 : 자료형이 다른 여러 데이터를 저장하는 변수
 * TYPE 레코드변수명 IS RECORD(
 * 변수이름 자료형 NOT NULL := 값;
 * 변수이름 자료형 NOT NULL := 값;
 */
-- 레코드 정의해서 사용하기
DECLARE
  TYPE REC_DEPT IS RECORD(
    deptno NUMBER(2) NOT NULL := 99,
    dname  DEPARTMENT.DNAME%TYPE,      -- 참조(references) 타입
    loc DEPARTMENT.LOC%TYPE
  );
  
  v_dept_rec REC_DEPT;
BEGIN
  v_dept_rec.deptno := 99;
  v_dept_rec.dname := 'DATABASE';
  v_dept_rec.loc := 'SEOUL';
  
  DBMS_OUTPUT.PUT_LINE('DEPTNO : ' || v_dept_rec.deptno);
  DBMS_OUTPUT.PUT_LINE('DNAME : ' || v_dept_rec.dname);
  DBMS_OUTPUT.PUT_LINE('LOC : ' || v_dept_rec.loc);
END;
/
```

* 레코드를 사용하여 테이블에 INSERT하기
```SQL
-- DEPT_RECORD 테이블 생성하기
CREATE TABLE DEPT_RECORD
AS SELECT * FROM DEPARTMENT;

SELECT * FROM DEPT_RECORD;

-- 레코드를 사용하여 INSERT하기
DECLARE
  TYPE REC_DEPT IS RECORD(
    deptno NUMBER(2) NOT NULL := 99,
    dname  DEPARTMENT.DNAME%TYPE,
    loc    DEPARTMENT.LOC%TYPE
  );
  dept_rec REC_DEPT;
BEGIN
  dept_rec.deptno := 99;
  dept_rec.dname  := 'DATABASE';
  dept_rec.loc    := 'SEOULT';
  
  INSERT INTO DEPT_RECORD
  VALUES dept_rec;
END;
/
```
```SQL
/*
 * 다음과 같은 결과가 나오도록 PL/SQL 문을 작성해 보세요
 * 1. EMP 테이블과 같은 열 구조를 가지는 빈 테이블 EMP_RECORD를 생성하는 SQL문 작성
 * 2. EMP_RECORD 테이블에 레코드를 사용하여 다음과 같은 값을 삽입 
 */ 
-- 테이블 생성
CREATE TABLE EMP_RECORD AS SELECT * FROM EMPLOYEE WHERE 1<>1;

-- 레코드를 사용하여 테이블에 데이터 삽입
DECLARE
  TYPE REC_EMP IS RECORD(
    empno       EMPLOYEE.ENO%TYPE NOT NULL := 9999,
    ename       EMPLOYEE.ENAME%TYPE,
    job         EMPLOYEE.JOB%TYPE,
    manager    EMPLOYEE.MANAGER%TYPE,
    hiredate    EMPLOYEE.HIREDATE%TYPE,
    salary      EMPLOYEE.SALARY%TYPE,
    commission  EMPLOYEE.COMMISSION%TYPE,
    deptno      EMPLOYEE.DNO%TYPE
  );
  emp_rec REC_EMP;
  
BEGIN
  emp_rec.empno := 1111;
  emp_rec.ename := 'TEST_USER';
  emp_rec.job := 'TEST_JOB';
  emp_rec.manager := null;
  emp_rec.hiredate := TO_DATE('20180301', 'YY/MM/DD');
  emp_rec.salary := 3000;
  emp_rec.commission := null;
  emp_rec.deptno := 40;
  
  INSERT INTO EMP_RECORD
  VALUES emp_rec;
END;
/
```
* 레코드를 사용하여 테이블 UPDATE하기
```SQL
-- 레코드를 사용하여 UPDATE하기
DECLARE
  TYPE REC_DEPT IS RECORD(
  deptno NUMBER(2) NOT NULL := 99,
  dname DEPARTMENT.DNAME%TYPE,
  loc   DEPARTMENT.LOC%TYPE
  );
  dept_rec REC_DEPT;
BEGIN
  dept_rec.deptno := 50;
  dept_rec.dname := 'DB';
  dept_rec.loc := 'SEOUL';
  
  UPDATE DEPT_RECORD
     SET ROW = dept_rec
   WHERE DNO = 99;
END;
/

```
* 레코드를 중첩하여 사용하기
```SQL
-- 레코드에 다른 레코드 포함하기
DECLARE
  TYPE REC_DEPT IS RECORD(
    deptno  DEPARTMENT.DNO%TYPE,
    dname   DEPARTMENT.DNAME%TYPE,
    loc     DEPARTMENT.LOC%TYPE
  );
  
  TYPE REC_EMP IS RECORD(
    empno   EMPLOYEE.ENO%TYPE,
    ename   EMPLOYEE.ENAME%TYPE,
    dinfo REC_DEPT
  );
  
  emp_rec REC_EMP;
BEGIN
  SELECT E.ENO, E.ENAME, D.DNO, D.DNAME, D.LOC
    INTO emp_rec.empno, emp_rec.ename
        , emp_rec.dinfo.deptno, emp_rec.dinfo.dname, emp_rec.dinfo.loc
    FROM EMPLOYEE E JOIN DEPARTMENT D ON(E.DNO = D.DNO)
   WHERE E.ENO = 7788;
   
   DBMS_OUTPUT.PUT_LINE('EMPNO : ' || emp_rec.empno);
   DBMS_OUTPUT.PUT_LINE('ENAME : ' || emp_rec.ename);
   
   DBMS_OUTPUT.PUT_LINE('D.DNO : ' || emp_rec.dinfo.deptno);
   DBMS_OUTPUT.PUT_LINE('D.DNAME : ' || emp_rec.dinfo.dname);
   DBMS_OUTPUT.PUT_LINE('D.LOC : ' || emp_rec.dinfo.loc);
END;
/
```

## 컬렉션
> 자료형이 같은 여러 데이터를 변수에 저장
### 연관배열(associative array (or index by table))
```SQL
-- 연관배열
TYPE 연관배열변수명 IS TABLE OF 자료형(NOT NULL)
INDEX BY 인덱스형(BINARY_INTEGER, PLS_INTEGER);
```

```SQL
-- 연관배열 사용하기
DECLARE
  TYPE ITAB_EX IS TABLE OF VARCHAR2(20)
  INDEX BY PLS_INTEGER;
  
  test_arr ITAB_EX;
BEGIN
  test_arr(1) := '1st data';
  test_arr(2) := '2nd data';
  test_arr(3) := '3rd data';
  test_arr(4) := '4th data';
  
  DBMS_OUTPUT.PUT_LINE('test_arr(1) : ' || test_arr(1));
  DBMS_OUTPUT.PUT_LINE('test_arr(2) : ' || test_arr(2));
  DBMS_OUTPUT.PUT_LINE('test_arr(3) : ' || test_arr(3));
  DBMS_OUTPUT.PUT_LINE('test_arr(4) : ' || test_arr(4));
END;
/
```
* 연관배열 자료형에 레코드 사용하기
```SQL
-- 연관배열 자료형에 레코드 사용하기
DECLARE
  TYPE REC_DEPT IS RECORD(
    deptno DEPARTMENT.DNO%TYPE,
    dname  DEPARTMENT.DNAME%TYPE
  );
  
  TYPE ITAB_DEPT IS TABLE OF REC_DEPT
  INDEX BY PLS_INTEGER;
  
  dept_arr ITAB_DEPT;
  idx PLS_INTEGER := 0;
BEGIN
  FOR i IN (SELECT DNO, DNAME FROM DEPARTMENT) LOOP
    idx := idx + 1;
    dept_arr(idx).deptno := i.DNO;
    dept_arr(idx).dname := i.DNAME;
    
    DBMS_OUTPUT.PUT_LINE(
      dept_arr(idx).deptno || ' - ' || dept_arr(idx).dname);
  END LOOP;
END;
/
```
```SQL
/*
 * EMP 테이블을 구성하는 모든 열을 저장할 수 있는 레코드를 활용
 * 연관 배열을 작성해 보세요. 그리고 저장된 연관 배열의 내용을 출력하세요.
 */
DECLARE
  TYPE ITAB_EMP IS TABLE OF EMPLOYEE%ROWTYPE
  INDEX BY PLS_INTEGER;
  
  emp_arr ITAB_EMP;
  idx PLS_INTEGER := 0;
BEGIN
  FOR i IN(SELECT * FROM EMPLOYEE) LOOP
    idx := idx + 1;
--    emp_arr(idx).eno := i.ENO;
--    emp_arr(idx).ename := i.ENAME;
--    emp_arr(idx).job := i.JOB;
--    emp_arr(idx).manager := i.MANAGER;
--    emp_arr(idx).hiredate := i.HIREDATE;
--    emp_arr(idx).salary := i.SALARY;
--    emp_arr(idx).commission := i.COMMISSION;
--    emp_arr(idx).dno := i.DNO;
    
    emp_arr(idx) := i;
    
  DBMS_OUTPUT.PUT_LINE(
    emp_arr(idx).eno || ' : ' ||
    emp_arr(idx).ename || ' : ' ||
    emp_arr(idx).job || ' : ' ||
    emp_arr(idx).manager || ' : ' ||
    emp_arr(idx).hiredate || ' : ' ||
    emp_arr(idx).salary || ' : ' ||
    emp_arr(idx).commission || ' : ' ||
    emp_arr(idx).dno
  );
  
  END LOOP;
END;
/
```
* %ROWTYPE으로 연관 배열 자료형 지정하기
```SQL
-- %ROWTYPE으로 연관 배열 자료형 지정하기
DECLARE
  TYPE ITAB_DEPT IS TABLE OF DEPARTMENT%ROWTYPE
  INDEX BY PLS_INTEGER;
  
  dept_arr ITAB_DEPT;
  idx PLS_INTEGER := 0;
BEGIN
  FOR i IN(SELECT * FROM DEPARTMENT) LOOP
    idx := idx + 1;
    dept_arr(idx).dno := i.DNO;
    dept_arr(idx).dname := i.DNAME;
    dept_arr(idx).loc := i.LOC;
    
    DBMS_OUTPUT.PUT_LINE(
      dept_arr(idx).dno || ' - ' ||
      dept_arr(idx).dname || ' - ' ||
      dept_arr(idx).loc
    );
    
  END LOOP;
END;
/
```

### 중첩 테이블(nested table)
> 중첩 테이블

### VARRAY(variable-size array)
> VARRAY

## 컬렉션 메서드
> 컬렉션에 공동으로 제공되는 메서드
```SQL
DECLARE
  TYPE ITAB_EX IS TABLE OF VARCHAR2(20)
  INDEX BY PLS_INTEGER;
  
  test_arr ITAB_EX;
BEGIN
  test_arr(1) := '1st data';
  test_arr(2) := '2nd data';
  test_arr(3) := '3rd data';
  test_arr(50) := '50th data';
  
  -- 컬렉션 메서드를 이용한 다양한 기능
  DBMS_OUTPUT.PUT_LINE('test_arr.COUNT : ' || test_arr.COUNT);         -- COUNT : 포함되어 있는 요소 개수 반환
  DBMS_OUTPUT.PUT_LINE('test_arr.FIRST : ' || test_arr.FIRST);         -- FIRST : 첫 번째 인덱스 번호 반환
  DBMS_OUTPUT.PUT_LINE('test_arr.LAST : ' || test_arr.LAST);           -- LAST  : 마지막 인덱스 번호 반환
  DBMS_OUTPUT.PUT_LINE('test_arr.PRIOR(50) : ' || test_arr.PRIOR(50)); -- PRIOR(n) : n인덱스 바로 앞 인덱스 값 반환
  DBMS_OUTPUT.PUT_LINE('test_arr.NEXT(50) : ' || test_arr.NEXT(50));   -- NEXT(n) : n인덱스 바로 다음 인덱스 값 반환
END;
/
```
