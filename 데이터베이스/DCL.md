# DCL
> DCL(데이터 제어 언어: Data Control Language)는 데이터베이스의 사용 권한을 관리하는 명령어의 집합

## GRANT
> GRANT 문을 사용하여 사용 권한 부여
```SQL
GRANT privilege_name,
TO user_name;
```

## 사용 권한 
> 사용 권한은 시스템 권한(System Privileges)과 객체 권한(Object Privileges)으로 나뉩니다.

## 시스템 권한

|시스템 권한|기능|
|---|---|
|CREATE SESSION|데이터베이스에 연결할 수 있는 권한|
|CREATE TABLE|테이블을 생성할 수 있는 권한|
|CREATE SEQUENCE|시퀀스를 생성할 수 있는 권한|
|CREATE VIEW|뷰를 생성할 수 있는 권한|
|CREATE SESSION|데이터베이스에 연결할 수 있는 권한|

### CREATE USER
> 권한을 가진 사용자를 생성합니다.
```SQL
 CREATE USER user_name
 IDENTIFIED BY password;
```
* 사용자 생성
```SQL
-- 권한이 있을 경우(SYS 계정)
CREATE USER ORCLSTUDY -- ID : ORCLSTUDY
IDENTIFIED BY ORACLE; -- PW : ORACLE

-- OUTPUT --
User ORCLSTUDY이(가) 생성되었습니다.

-- 권한이 없을 경우(HR 계정)
CREATE USER ORCLSTUDY
IDENTIFIED BY ORACLE;

-- ERROR --
insufficient privileges
```

* 사용자 검색
```SQL
SELECT * FROM ALL_USERS
 WHERE USERNAME = 'ORCLSTUDY';
```

* 사용자 암호 변경
```SQL
ALTER USER ORCLSTUDY
IDENTIFIED BY ORCL;
```

* 사용자 삭제
```SQL
DROP USER ORCLSTUDY;

-- 사용자와 객체(데이터 사전, 인덱스, 시퀀스 등) 모두 삭제
DROP USER ORCLSTUDY CASCADE;
```

### CREATE SESSION
> 새로 생성된 사용자에 데이터베이스 관리자를 접속할 수 있는 권한을 부여합니다.
```SQL
GRANT CREATE SESSION TO ORCLSTUDY;
```

### CREATE TABLE
> 사용자에게 테이블 생성 권한을 부여합니다.
```SQL
GRANT RESOURCE, CREATE SESSION, CREATE TABLE TO ORCLSTUDY;
```

## 객체 권한
> 특정 객체에 조작을 할 수 있는 권한

|권한|TABLE|VIEW|SEQUENCE|PROCEDURE|
|---|---|---|---|---|
|ALTER|V||V||
|DELETE|V||V||
|EXECUTE||||V|
|INDEX|V||||
|INSERT|V|V|||
|REFERENCES|V||||
|SELECT|V|V|V||
|UPDATE|V|V|||

* 객체 권한은 객체(테이블, 뷰, 시퀀스, 함수)별로 DML문을 사용할 수 있는 권한을 설정
```SQL
-- 객체에 권한을 부여하기 위한 형식
GRANT privilege_name [(column_name)] | ALL -- 1.
ON object_name | role_name | PUBLIC -- 2.
TO user_name -- 3.
```
> 어떤 객체(2.)에 어떠한 권한(1.)을 어느 사용자(3.)에게 부여하는가를 설정합니다.
* 객체 권한 부여는 시스템 권한과 다르게 ON 옵션이 추가됩니다. ON 다음 객체의 종류를 기술합니다.

```SQL
-- ORCLSTUDY에게 HR 계정의 TEMP 테이블 SELECT, INSERT 권한 부여
GRANT SELECT, INSERT
ON TEMP 
TO ORCLSTUDY;

-- ORCLSTUDY 계정에 접속
INSERT INTO HR.TEMP VALUES('TEST', 'FROM ORCLSTUDY'); -- HR.TEMP: HR 계정의 TEMP TABLE

-- HR 계정에 접속
SELECT * FROM TEMP;

-- OUTPUT --
COL1                 COL2                
-------------------- --------------------
TEST                 FROM ORCLSTUDY      
```
## REVOKE
> REVOKE 문을 사용하여 사용자에게 부여한 사용 권한을 박탈합니다.
```SQL
REVOKE {privilege_name | all}
ON object_name
FROM {user_name | role_name | public};
```
```SQL
-- RESOURCE, CREATE TABLE 권한 박탈
REVOKE RESOURCE, CREATE TABLE FROM ORCLSTUDY;

SQL> CREATE TABLE TEMP3(
       COL1 VARCHAR(20),
       COL2 VARCHAR(20)
     );
     
-- ERROR --
insufficient privileges
```
## WITH GRANT OPTION
* 사용자에게 객체 권한을 WITH GRANT OPTION과 함께 부여하면 그 사용자는 그 객체를 접근할 권한을 부여 받으면서 그 권한을 다른 사용자에게 부여할 수 있습니다.

## 롤
> 여러 사용자에게 권한을 부여하고 수정할 때 일일이 사용자마다 권한을 수정할 필요 없이 롤을 통해 부여하면 롤의 권한을 수정하면 롤을 통해 부여된 객체들의 권한이 자동으로 수정됩니다.

|롤 종류|롤에 부여된 권한|
|---|---|
|DBA|WITH ADMIN OPTION에 있는 모든 권한|
|CONNECT|ALTER SESSION, CREATE CLUSTER, CREATE DATABASE LINK, CREATE SEQUENCE, CREATE SESSION, CREATE SYNONYM, CREATE TABLE, CREATE VIEW|
|RESOURCE|CREATE CLUSTER, CREATE PROCEDURE, CREATE SEQUENCE, CREATE TABLE, CREATE TRIGGER|
* 롤 생성
```SQL
CREATE ROLE ROLESTUDY;

GRANT CONNECT, RESOURCE, CREATE VIEW, CREATE SYNONYM
   TO ROLESTUDY;
```
* 롤 권한 부여
```SQL
GRANT ROLESTUDY TO ORCLSTUDY;
```

* 롤 권한 박탈
```SQL
REVOKE ROLESTUDY FROM ORCLSTUDY;
```

* 롤 삭제
```SQL
DROP ROLE ROLESTUDY;
```

### 롤 관련 데이터 사전
|사전 명|설명|
|---|---|
|ORLE_SYS_PRIVS|롤에 부여된 시스템 권한 정보|
|ROLE_TAB_PRIVS|롤에 부여된 테이블 관련 권한 정보|
|USER_ROLE_PRIVS|접근 가능한 롤 정보|
|USER_TAB_PRIVS_MADE|해당 사용자 소유의 오브젝트에 대한 오브젝트 권한 정보|
|USER_TAB_PRIVS_RECD|사용자에게 부여된 오브젝트 권한 정보|
|USER_COL_PRIVS_MADE|사용자 소유의 오브젝트 중 칼럼에 부여된 오브젝트 권한 정보|
|USER_COL_PRIVS_RECD|사용자에게 부여된 특정 칼럼에 대한 오브젝트 권한 정보|
* USER_SYS_PRIVS
```SQL
SELECT * FROM USER_SYS_PRIVS;

-- OUTPUT --
USERNAME                                                     PRIVILEGE                                                                        ADMIN_
------------------------------------------------------------ -------------------------------------------------------------------------------- ------
ORCLSTUDY                                                    CREATE SESSION                                                                   NO

```
* USER_ROLE_PRIVS
```SQL
SELECT * FROM USER_ROLE_PRIVS;

-- OUTPUT --
USERNAME                                                     GRANTED_ROLE                                                 ADMIN_ DEFAUL OS_GRA
------------------------------------------------------------ ------------------------------------------------------------ ------ ------ ------
ORCLSTUDY                                                    ROLESTUDY                                                    NO     YES    NO
```

## SYNONYM
> 동의어는 다른 데이터베이스 객체에 대한 별칭입니다.  
> 접근 권한을 부여받은 사용자만 사용 가능한 비공개 동의어와 누구나 접근 가능한 공개 동의어가 있습니다.
* SYNONYM 권한 부여
```SQL
-- SYS계정에서 해당 테이블에 권한 부여
GRANT CREATE SYNONYM TO HR;

GRANT CREATE PUBLIC SYNONYM TO HR;
-- HR 계정에서 SYNONYM 생성
```

* SYNONYM 생성
```SQL
-- SYNONYM 생성
CREATE SYNONYM EMP
FOR EMPLOYEE;

SELECT * FROM EMP; 
```

* SYNONYM 삭제
```SQL
DROP SYNONYM EMP;
```

# 트랜잭션(Transaction)
* 트랜잭션은 데이터 처리에서 논리적으로 하나의 단위를 의미
* oracle 명령어 중 DDL과 DCL은 하나의 명령어가 하나의 트랜잭션이며, DML은 데이터의 변동의 일관성을 위해 하나 이상의 DML문이 모여 하나의 트랜잭션을 구성
* ALL - OR - Nothing: 여러 개의 명령어 집합이 정상적으로 처리되면 정상 종료, 명령어들 중 하나라도 잘못되면 전체를 취소

* DML문은 실행됨과 동시에 트랜잭션이 진행됩니다. DML 작업이 성공적으로 처리되었다면 COMMIT을, 취소해야 한다면 ROLLBACK 명령을 실행
* COMMIT은 트랜잭션의 처리 과정을 반영하여 변경된 내용을 모두 영구 저장
* ROLLBACK은 트랜잭션의 처리 과정 중 발생한 변경 사항을 취소하는 명령어입니다. ROLLBACK을 실행하게 되면 하나의 묶음 처리가 시작되기 이전 상태로 돌아갑니다.