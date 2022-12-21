# DDL
> DDL(데이터 정의어 : Data Definition Language)은 테이블을 수정, 제거하도록 하는 명령문 집합

> 즉, 데이터 관리, 보관을 위해 객체를 제공하며 이런 객체를 새로 만들거나 기존에 존재하는 객체를 변경, 삭제하는 명령어

* DDL은 ROLLBACK을 통한 실행 취소가 불가
* 테이블 이름 생성 규칙 : 영문자, 숫자, $, #, _ 가능

## CREATE 문
> 데이터를 저장할 테이블을 생성

```SQL
 CREATE TABLE [schema.] table
       (column datatype [DEFAULT expression]
       [column_constraint clause] [,...]);
```
* schema : 소유자의 이름(사용자 계정)
* column : 테이블에 포함되는 칼럼명
* datatype : 칼럼에 대한 데이터 타입과 길이
* DEFAULT expression : 데이터 입력 값에 생략된 경우 입력되는 기본 값
* column_constraint_clause : 칼럼에 정의되는 무결성 제약 조건

### [CREATE를 이용한 테이블 생성 방법]
* 모든 열의 각 자료형을 정의해서 테이블을 생성
```SQL
 CREATE TABLE EMP_DDL(
    ENO NUMBER(4),
    ENAME VARCHAR2(10),
    JOB VARCHAR2(9),
    MANAGER NUMBER(4),
    HIREDATE DATE,
    SALARY NUMBER(7, 2),
    COMMISSION NUMBER(7, 2),
    DNO NUMBER(2)
);
```
* 기존 테이블 열 구조와 일부 데이터만 복사하여 테이블 생성
```SQL
 CREATE TABLE EMP_DDL_30
     AS SELECT *
          FROM EMPLOYEE
         WHERE DNO = 30;
```
* 기존 테이블의 열 구조만 복사하여 테이블 생성
```SQL
 CREATE TABLE EMPDEPT_DDL
 AS SELECT E.ENO, E.ENAME, E.JOB, E.MANAGER, E.HIREDATE
          , E.SALARY, E.COMMISSION, D.DNO, D.DNAME, D.LOC
      FROM EMPLOYEE E, DEPARTMENT D
     WHERE 1 != 1;
```
* 서브쿼리를 사용하여 테이블 생성
```SQL
 CREATE TABLE table [column [,column, ...]]
 AS subquery;
```
> 칼럼명을 명시적으로 언급할 경우 지정한 칼럼 수, 데이터 타입이 서브쿼리와 일치해야 하며 언급하지 않을 경우 서브쿼리의 칼럼명이 그대로 기입

## ALTER 문
> 테이블의 칼럼을 추가, 수정, 삭제

```SQL
 ALTER TABLE table_name
   ADD ([column_name data_type DEFAULT expr]
        [, column_name data_type] ... );
```
* ADD를 사용하여 새로운 칼럼 추가
```SQL
 -- ALTER 명령어로 HP 열 추가하기
 ALTER TABLE EMP_ALTER
   ADD HP VARCHAR2(20);
```
* MODIFY를 사용하여 칼럼 변경
```SQL
  ALTER TABLE EMP_ALTER
 MODIFY ENO NUMBER(5);
```
> 기존 칼럼에 데이터가 없는 경우 칼럼 타입 및 크기 변경은 자유롭습니다.

> 데이터가 존재하는 경우 타입 변경은 CHAR, VARCHAR2만 허용되며 변경한 칼럼의 크기는 저장된 데이터의 크기와 같거나 클 경우만 변경 가능합니다.

> 숫자 타입은 폭 혹은 전체 자릿수를 늘릴 수 있습니다.

* RENAME을 사용하여 칼럼 이름 변경
```SQL
 -- ALTER 명령어로 HP열 이름을 TEL로 변경하기
  ALTER TABLE EMP_ALTER
 RENAME COLUMN HP TO TEL;
```
* DROP을 사용하여 칼럼 삭제
```SQL
 ALTER TABLE EMP_ALTER
  DROP COLUMN TEL;
```

## RENAME 문
> 테이블을 포함한 모든 객체의 이름을 변경
```SQL
 -- EMP_ALTER 테이블에서 EMP_RENAME 테이블로 변경
 RENAME EMP_ALTER TO EMP_RENAME;
```

## DROP 문
> 기존의 테이블과 데이터를 모두 제거
* 삭제할 테이블의 기본 키나 고유 키를 다른 테이블에서 참조하고 있는 경우 삭제가 불가능, 그럴 경우 참조 중인 자식 테이블을 먼저 제거
```SQL
 DROP TABLE EMP_RENAME;
```

## TRUNCATE 문
> 기존의 테이블의 모든 로우를 제거
* 테이블의 구조는 그대로 유지, 테이블의 데이터와 이에 할당된 공간 해제
* 제약 조건, 인덱스, 뷰, 동의어 등은 그대로 유지
```SQL
 TRUNCATE TABLE EMP_RENAME;
```

## SET UNUSED
* 시스템 요구가 적을 때 칼럼을 제거할 수 있도록 하나 이상의 칼럼을 UNUSED로 표시(실제로는 테이블에서 삭제되지 않음)
* DROP 명령보다 응답시간이 빠름
* 삭제된 것으로 처리하기 때문에 SELECT나 DESCRIBE를 사용할 수 없음