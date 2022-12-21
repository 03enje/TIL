# DQL(Data Query Language)
테이블 내의 데이터를 조회하는 명령어입니다.

## 📂 SELECT 문

✔ 데이터베이스 내에 저장되어있는 테이블의 데이터를 조회하기 위한 명령어입니다.  

```SQL
SELECT [DISTINCT] {*, column[Alias], ...} -- 칼럼명의 리스트 나열 [DISTINCT 사용 시 중복값 제거]
FROM table_name -- 테이블명의 리스트 나열
[WHERE condition] -- 로우의 조건 나열
[GROUP BY group_by_expression] -- 동일한 값을 갖는 로우들의 그룹
[Having group_condition] -- 로우들의 그룹 조건 제시
[ORDER BY column] -- 로우들의 정렬 순서 제시 [ASC(기본값) : 오름차순, DESC : 내림차순]
```

✔ SELECT 다음에 '*'을 기술하면 지정된 테이블의 모든 칼럼을 조회합니다.  

✔ FROM 다음에는 보고자 하는 대상의 테이블 이름을 기술합니다.

## 📂 WHERE 절

✔ 특정 조건의 데이터(로우)만 조회합니다.

✔ 데이터 조회시 문자 상수임을 알리기 위해 작은 따옴표를 사용합니다.

```SQL
SELECT *
  FROM employee
 WHERE ename = 'SCOTT' -- 문자열에 작은 따옴표 사용
```

### 📄 비교 연산자

|연산자|의미|
|---|---|
|=|같다|
|>|보다 크다(초과)|
|<|보다 작다(미만)|
|>=|보다 크거나 같다(이상)|
|<=|보다 작거나 같다(이하)|
|<>, !=, ^=|다르다|

<hr/>

### 📄 논리 연산자

|연산자|의미|
|------|------|
|AND|두 가지 조건을 모두 만족해야만 검색할 수 있습니다.|
|OR|두 가지 조건 중에서 한 가지만 만족하더라도 검색할 수 있습니다.|
|NOT|조건에 만족하지 못하는 것만 검색합니다.|

<hr/>

### 📄 BETWEEN AND 연산자
◽ 특정 칼럼의 데이터 값이 하한가(A)와 상한값(B) 사이에 포함되는 로우를 검색하기 위한 연산자입니다.

<details>
<summary>🔎예제 코드 확인</summary>

```SQL
SELECT * FROM employee
 WHERE salary BETWEEN 1000 AND 1500;

출력:
       ENO ENAME                JOB                   MANAGER HIREDATE     SALARY COMMISSION        DNO
---------- -------------------- ------------------ ---------- -------- ---------- ---------- ----------
      7521 WARD                 SALESMAN                 7698 81/02/22       1250        500         30
      7654 MARTIN               SALESMAN                 7698 81/09/28       1250       1400         30
      7844 TURNER               SALESMAN                 7698 81/09/08       1500          0         30
...
```

</details>

<hr/>

### 📄 IN 연산자
◽ 특정 칼럼의 값이 A, B, C 중에 하나라도 일치하면 참이 되는 연산자입니다.

<details>
<summary>🔎예제 코드 확인</summary><br>

```SQL
SELECT * FROM employee
 WHERE commission IN(300, 500, 1400);

출력:
       ENO ENAME                JOB                   MANAGER HIREDATE     SALARY COMMISSION        DNO
---------- -------------------- ------------------ ---------- -------- ---------- ---------- ----------
      7499 ALLEN                SALESMAN                 7698 81/02/20       1600        300         30
      7521 WARD                 SALESMAN                 7698 81/02/22       1250        500         30
      7654 MARTIN               SALESMAN                 7698 81/09/28       1250       1400         30
```

</details>

<hr/>

### 📄 LIKE 연산자
◽ 칼럼에 저장된 문자상수 중에서 LIKE 연산자에서 지정한 문자패턴과 부분적으로 일치하면 참이 되는 연산자입니다.

<details>
<summary>🔎예제 코드 확인</summary><br>

```SQL
SELECT * FROM employee
 WHERE ename LIKE 'F%';

출력:
       ENO ENAME                JOB                   MANAGER HIREDATE     SALARY COMMISSION        DNO
---------- -------------------- ------------------ ---------- -------- ---------- ---------- ----------
      7902 FORD                 ANALYST                  7566 81/12/03       3000                    20
```

```SQL
SELECT * FROM employee
 WHERE ename LIKE '_A%';

출력:
       ENO ENAME                JOB                   MANAGER HIREDATE     SALARY COMMISSION        DNO
---------- -------------------- ------------------ ---------- -------- ---------- ---------- ----------
      7521 WARD                 SALESMAN                 7698 81/02/22       1250        500         30
      7654 MARTIN               SALESMAN                 7698 81/09/28       1250       1400         30
      7900 JAMES                CLERK                    7698 81/12/03        950                    30
```

</details>

#### 📑 와일드카드

|와일드카드|의미|
|---|---|
|%|문자가 없거나, 하나 이상의 문자가 어떤 값이 와도 상관없습니다.|
|_|하나의 문자가 어떤 값이 와도 상관없습니다.|

<hr/>

### 📄 IS NULL, IS NOT NULL
◽ 어떤한 칼럼이 NULL일 경우 IS NULL 연산자를 사용해야 합니다. 반대로 NOT을 사용할 수도 있습니다.

<details>
<summary>🔎예제 코드 확인</summary><br>

```SQL
SELECT * FROM employee
 WHERE commission IS NULL;

출력:
       ENO ENAME                JOB                   MANAGER HIREDATE     SALARY COMMISSION        DNO
---------- -------------------- ------------------ ---------- -------- ---------- ---------- ----------
      7369 SMITH                CLERK                    7902 80/12/17        800                    20
      7566 JONES                MANAGER                  7839 81/04/02       2975                    20
      7698 BLAKE                MANAGER                  7839 81/05/01       2850                    30
...
```

```SQL
SELECT * FROM employee
 WHERE commission IS NOT NULL;

출력:
       ENO ENAME                JOB                   MANAGER HIREDATE     SALARY COMMISSION        DNO
---------- -------------------- ------------------ ---------- -------- ---------- ---------- ----------
      7499 ALLEN                SALESMAN                 7698 81/02/20       1600        300         30
      7521 WARD                 SALESMAN                 7698 81/02/22       1250        500         30
      7654 MARTIN               SALESMAN                 7698 81/09/28       1250       1400         30
      7844 TURNER               SALESMAN                 7698 81/09/08       1500          0         30
```

</details>

## 📂 ORDER BY 절
✔ 크기 순서대로 로우들을 정렬합니다. [ASC(기본값) : 오름차순, DESC : 내림차순]

✔ ASC는 오름차순으로 정렬합니다.
```SQL
SELECT * FROM employee
 WHERE commission IS NOT NULL
 ORDER BY commission ASC;
 
출력:
       ENO ENAME      JOB          MANAGER HIREDATE       SALARY COMMISSION        DNO
---------- ---------- --------- ---------- ---------- ---------- ---------- ----------
      7844 TURNER     SALESMAN        7698 1981-09-08       1500          0         30
      7499 ALLEN      SALESMAN        7698 1981-02-20       1600        300         30
      7521 WARD       SALESMAN        7698 1981-02-22       1250        500         30
      7654 MARTIN     SALESMAN        7698 1981-09-28       1250       1400         30
```
✔ DESC는 내림차순으로 정렬합니다.
```SQL
SELECT * FROM employee
 WHERE commission IS NOT NULL
 ORDER BY commission DESC;
 
출력:
       ENO ENAME      JOB          MANAGER HIREDATE       SALARY COMMISSION        DNO
---------- ---------- --------- ---------- ---------- ---------- ---------- ----------
      7654 MARTIN     SALESMAN        7698 1981-09-28       1250       1400         30
      7521 WARD       SALESMAN        7698 1981-02-22       1250        500         30
      7499 ALLEN      SALESMAN        7698 1981-02-20       1600        300         30
      7844 TURNER     SALESMAN        7698 1981-09-08       1500          0         30
```

✔ ORDER BY를 기술하지 않으면 디폴트값인 ASC로 오름차순 정렬합니다.