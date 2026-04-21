# EXPERIMENT-
# 01. Delete those employees who joined the company before 31 dec-82 while there dept location is ‘DELHI’ or ‘CHENNAI’.
 Query
~~~sql   
DELETE FROM EMPLOYEE
WHERE HIREDATE < '1982-12-31'
AND DEPTNO IN (SELECT DEPTNO FROM DEPARTMENT
    WHERE LOCATION IN ('DELHI', 'CHENNAI'));

SELECT * FROM EMPLOYEE;
~~~
 Output
~~~SQL
Query OK, 6 rows affected (0.011 sec)
+-------+--------+----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB      | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+----------+------+------------+------+------+--------+
|  7499 | ALLEN  | SELESMAN | 7698 | 1981-02-20 | 1600 |  300 |     30 |
|  7521 | WARD   | SELESMAN | 7698 | 1981-02-22 | 1250 |  300 |     30 |
|  7654 | MARTIN | SELESMAN | 7698 | 1981-09-28 | 1250 | 1400 |     30 |
|  7698 | BLAKE  | MANAGER  | 7839 | 1981-03-01 | 2850 | NULL |     30 |
|  7844 | TURNER | SELESMAN | 7698 | 1981-09-08 | 1500 |    0 |     30 |
|  7876 | ADAMS  | CLERK    | 7788 | 1983-01-12 | 1100 | NULL |     20 |
|  7900 | JAMES  | CLERK    | 7698 | 1981-12-03 |  950 | NULL |     30 |
|  7934 | MILLER | CLERK    | 7782 | 1982-01-23 | 1300 | NULL |     10 |
+-------+--------+----------+------+------------+------+------+--------+

~~~
# 02. Display employee name, job, deptname, location for all who are working as managers. 
 Query
~~~sql   
 SELECT E.ENAME,E.JOB,D.DNAME,D.LOCATION
    -> FROM EMPLOYEE E
    -> JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
    -> WHERE E.JOB = 'MANAGER';
~~~
 Output
~~~SQL
+-------+---------+------------+-----------+
| ENAME | JOB     | DNAME      | LOCATION  |
+-------+---------+------------+-----------+
| JONES | MANAGER | ACCOUNTING | CHENNAI   |
| CLARK | MANAGER | ACCOUNTING | CHENNAI   |
| BLAKE | MANAGER | SALES      | HYDERABAD |
+-------+---------+------------+-----------+
~~~
# 03. Display name and salary of ford if his sal is equal to high sal of his grade.
 Query
~~~sql   
SELECT E.ENAME, E.SAL FROM EMPLOYEE E
    -> JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
    -> WHERE E.ENAME = 'FORD'
    -> AND E.SAL = (SELECT MAX(E2.SAL) FROM EMPLOYEE E2
    ->     JOIN SALGRADE S2 ON E2.SAL BETWEEN S2.LOSAL AND S2.HISAL
    ->     WHERE S2.GRADE = S.GRADE);
~~~
 Output
~~~SQL
+-------+------+
| ENAME | SAL  |
+-------+------+
| FORD  | 3000 |
+-------+------+
~~~
# 04. Find out the top 5 earner of company.
 Query
~~~sql   
SELECT ENAME, SAL FROM EMPLOYEE
    -> ORDER BY SAL DESC
    -> LIMIT 5;
~~~
 Output
~~~SQL
+-------+------+
| ENAME | SAL  |
+-------+------+
| KING  | 5000 |
| FORD  | 3000 |
| SCOTT | 3000 |
| JONES | 2975 |
| BLAKE | 2850 |
+-------+------+
~~~
# 05. Display the name of those employees who are getting highest salary.
 Query
~~~sql   
SELECT ENAME FROM EMPLOYEE
    -> WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE);
~~~
 Output
~~~SQL
+-------+
| ENAME |
+-------+
| KING  |
+-------+
~~~
# 06.  Display those employees whose salary is equal to average of maximum and minimum.
 Query
~~~sql   
SELECT ENAME, SAL FROM EMPLOYEE
    -> WHERE SAL = ((SELECT MAX(SAL) FROM EMPLOYEE) +(SELECT MIN(SAL) FROM EMPLOYEE)) / 2;
~~~
 Output
~~~SQL
Empty set (0.004 sec)
~~~
# 07.Display dname where at least 3 are working and display only dname
 Query
~~~sql   
 SELECT D.DNAME FROM DEPARTMENT D
    -> JOIN EMPLOYEE E ON D.DEPTNO = E.DEPTNO
    -> GROUP BY D.DNAME
    -> HAVING COUNT(*) >= 3;
~~~
 Output
~~~SQL
+------------+
| DNAME      |
+------------+
| ACCOUNTING |
| SALES      |
+------------+
~~~
# 08. Display name of those managers names whose salary is more than average salary of company.
 Query
~~~sql   
SELECT ENAME FROM EMPLOYEE
    -> WHERE JOB = 'MANAGER'
    -> AND SAL > (SELECT AVG(SAL) FROM EMPLOYEE);
~~~
 Output
~~~SQL
+-------+
| ENAME |
+-------+
| JONES |
| BLAKE |
| CLARK |
+-------+
~~~
# 09.Display those managers name whose salary is more than an average salary of his employees. 
 Query
~~~sql   
 SELECT M.ENAME FROM EMPLOYEE M
    -> WHERE M.JOB = 'MANAGER'
    -> AND M.SAL > (SELECT AVG(E.SAL)FROM EMPLOYEE E
    ->     WHERE E.MGR = M.EMPNO);
~~~
 Output
~~~SQL
+-------+
| ENAME |
+-------+
| BLAKE |
| CLARK |
+-------+
~~~
# 10. Display employee name, sal, comm and net pay for those employees whose net pay are greater than or equal to any other employee salary of the company?
 Query
~~~sql   
 SELECT ENAME, SAL, COMM,
    ->        (SAL + IFNULL(COMM,0)) AS NET_PAY
    -> FROM EMPLOYEE
    -> WHERE (SAL + IFNULL(COMM,0)) >= ANY (
    ->     SELECT SAL FROM EMPLOYEE);
~~~
 Output
~~~SQL
+--------+------+------+---------+
| ENAME  | SAL  | COMM | NET_PAY |
+--------+------+------+---------+
| SMITH  |  800 | NULL |     800 |
| ALLEN  | 1600 |  300 |    1900 |
| WARD   | 1250 |  300 |    1550 |
| JONES  | 2975 | NULL |    2975 |
| MARTIN | 1250 | 1400 |    2650 |
| BLAKE  | 2850 | NULL |    2850 |
| CLARK  | 2450 | NULL |    2450 |
| SCOTT  | 3000 | NULL |    3000 |
| KING   | 5000 | NULL |    5000 |
| TURNER | 1500 |    0 |    1500 |
| ADAMS  | 1100 | NULL |    1100 |
| JAMES  |  950 | NULL |     950 |
| FORD   | 3000 | NULL |    3000 |
| MILLER | 1300 | NULL |    1300 |
+--------+------+------+---------+
~~~
