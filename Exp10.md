# EXPERIMENT-10
# 01. Display the names of employees from department number 10 with salary greater than that of any employee working in other departments.
 Query
~~~sql   
 SELECT ENAME FROM EMPLOYEE
    -> WHERE DEPTNO = 10
    -> AND SAL > ANY (SELECT SAL FROM EMPLOYEE WHERE DEPTNO <> 10);
~~~
 Output
~~~SQL
+--------+
| ENAME  |
+--------+
| MILLER |
+--------+
~~~
# 02. Display the names of employee from department number 10 with salary greater than that of all employee working in other departments.
 Query
~~~sql   
 SELECT ENAME FROM EMPLOYEE
    -> WHERE DEPTNO = 10
    -> AND SAL > ALL ( SELECT SAL FROM EMPLOYEE WHERE DEPTNO <> 10);
~~~
 Output
~~~SQL
Empty set (0.008 sec)
~~~
# 03. Display the details of employees who are in sales dept and grade is C.
 Query
~~~sql   
 SELECT E.* FROM EMPLOYEE E
    -> JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
    -> JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
    -> WHERE D.DNAME = 'SALES'
    -> AND S.GRADE = 'C';
~~~
 Output
~~~SQL
+-------+--------+----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB      | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+----------+------+------------+------+------+--------+
|  7499 | ALLEN  | SELESMAN | 7698 | 1981-02-20 | 1600 |  300 |     30 |
|  7844 | TURNER | SELESMAN | 7698 | 1981-09-08 | 1500 |    0 |     30 |
+-------+--------+----------+------+------------+------+------+--------+
~~~
# 04. Display those who are not managers and who manages anyone.
 Query
~~~sql   
 SELECT ENAME FROM EMPLOYEE
    -> WHERE JOB != 'MANAGER'
    -> AND EMPNO IN ( SELECT MGR FROM EMPLOYEE WHERE MGR IS NOT NULL);
~~~
 Output
~~~SQL
+-------+
| ENAME |
+-------+
| SCOTT |
| KING  |
| FORD  |
+-------+
~~~
# 05. Display those employees whose manager name is jones.
 Query
~~~sql   
 SELECT E.ENAME FROM EMPLOYEE E 
    -> JOIN EMPLOYEE M ON E.MGR = M.EMPNO
    -> WHERE M.ENAME = 'JONES';
~~~
 Output
~~~SQL
+-------+
| ENAME |
+-------+
| SCOTT |
| FORD  |
+-------+
~~~
# 06. Display ename who are working in sales dept.
 Query
~~~sql   
SELECT E.ENAME FROM EMPLOYEE E
    -> JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
    -> WHERE D.DNAME = 'SALES';
~~~
 Output
~~~SQL
+--------+
| ENAME  |
+--------+
| ALLEN  |
| WARD   |
| MARTIN |
| BLAKE  |
| TURNER |
| JAMES  |
+--------+
~~~
# 07. Display employee name, deptname, salary and comm. For those sal in between 2000 to 5000 while location is Mumbai. 
 Query
~~~sql   
 SELECT E.ENAME, D.DNAME, E.SAL, E.COMM
    -> FROM EMPLOYEE E
    -> JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
    -> WHERE E.SAL BETWEEN 2000 AND 5000
    -> AND D.LOCATION = 'MUMBAI';
~~~
 Output
~~~SQL
Empty set (0.002 sec)
~~~
# 08. Display those employees whose salary greater than his manager salary.
 Query
~~~sql   
SELECT E.ENAME FROM EMPLOYEE E
    -> JOIN EMPLOYEE M ON E.MGR = M.EMPNO
    -> WHERE E.SAL > M.SAL;
~~~
 Output
~~~SQL
+-------+
| ENAME |
+-------+
| SCOTT |
| FORD  |
+-------+
~~~
# 09. Display those employees who are working in the same dept where his manager is working.
 Query
~~~sql   
 SELECT E.ENAME FROM EMPLOYEE E
    -> JOIN EMPLOYEE M ON E.MGR = M.EMPNO
    -> WHERE E.DEPTNO = M.DEPTNO;
~~~
 Output
~~~SQL
+--------+
| ENAME  |
+--------+
| SMITH  |
| ALLEN  |
| WARD   |
| JONES  |
| MARTIN |
| CLARK  |
| TURNER |
| JAMES  |
| FORD   |
+--------+
~~~
# 10. Display grade and employees name for the dept no 10 or 30 but grade is not D, while joined the company before 31-dec-82.
 Query
~~~sql   
SELECT E.ENAME, S.GRADE FROM EMPLOYEE E
    -> JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
    -> WHERE E.DEPTNO IN (10, 30)
    -> AND S.GRADE != 'D'
    -> AND E.HIREDATE < '1982-12-31';
~~~
 Output
~~~SQL
+--------+-------+
| ENAME  | GRADE |
+--------+-------+
| ALLEN  | C     |
| WARD   | B     |
| MARTIN | B     |
| TURNER | C     |
| JAMES  | A     |
| MILLER | B     |
+--------+-------+
~~~
