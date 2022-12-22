# ROWNUM
```SQL
 -- ROWNUM
 -- ORDER BY로 정렬해도 ROWNUM의 순서는 변하지 않음
 SELECT ROWNUM, E.*
   FROM EMPLOYEE E
  ORDER BY SALARY DESC;
  
 -- ROWNUM을 원하는 조건으로 정렬하고 싶으면
 -- ROWNUM을 호출하기 전 먼저 정렬을 해줘야 한다 
 SELECT ROWNUM, E.*
   FROM (SELECT *
           FROM EMPLOYEE E
          ORDER BY SALARY DESC) E;
   
   
WITH E AS (
 
    SELECT * 
      FROM EMPLOYEE 
     ORDER BY SALARY DESC
    
)
 
SELECT ROWNUM, E.*
  FROM E;

-- ROWNUM을 3위 이내로  
SELECT ROWNUM, E.*
  FROM (SELECT *
          FROM EMPLOYEE E
         ORDER BY SALARY DESC) E
         
 WHERE ROWNUM <= 3;
 
-- WITH 절을 사용하여 동일한 기능 구현
WITH E AS (

    SELECT *
      FROM EMPLOYEE
     ORDER BY SALARY DESC
    
)
SELECT ROWNUM, E.*
  FROM E
 WHERE ROWNUM <= 3;
 
```