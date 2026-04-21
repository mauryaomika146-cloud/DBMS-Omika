# EXPERIMENT- 9
# 01. Display the name of emp name who earns highest salary.
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
# 02. Display the employee number and name of employee working as clerk and earning highest salary among clerks.
 Query
~~~sql   
SELECT EMPNO, ENAME FROM EMPLOYEE
    -> WHERE JOB = 'CLERK'
    -> AND SAL = ( SELECT MAX(SAL)FROM EMPLOYEE WHERE JOB = 'CLERK');
~~~
 Output
~~~SQL
+-------+--------+
| EMPNO | ENAME  |
+-------+--------+
|  7934 | MILLER |
+-------+--------+
~~~
# 03. Display the names of the salesman who earns a salary more than the highest salary of any clerk.
 Query
~~~sql   
SELECT ENAME FROM EMPLOYEE
    -> WHERE JOB = 'SALESMAN'
    -> AND SAL > (SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB = 'CLERK');
~~~
 Output
~~~SQL
Empty set (0.003 sec)
~~~
# 04. Display the names of clerks who earn salary more than that of james of that of sal lesser than that of scott.
 Query
~~~sql   
SELECT ENAME FROM EMPLOYEE
    -> WHERE JOB = 'CLERK'
    -> AND SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'JAMES')
    -> AND SAL < (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'SCOTT');
~~~
 Output
~~~SQL
+--------+
| ENAME  |
+--------+
| ADAMS  |
| MILLER |
+--------+
~~~
# 05. Display the names of employees who earn a sal more than that of james or that of salary greater than that of scott.
 Query
~~~sql   
SELECT ENAME FROM EMPLOYEE
    -> WHERE SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'JAMES')
    -> OR SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'SCOTT');
~~~
 Output
~~~SQL
+--------+
| ENAME  |
+--------+
| ALLEN  |
| WARD   |
| JONES  |
| MARTIN |
| BLAKE  |
| CLARK  |
| SCOTT  |
| KING   |
| TURNER |
| ADAMS  |
| FORD   |
| MILLER |
+--------+
~~~
# 06. Display the names of the employees who earn highest salary in their respective departments. 
 Query
~~~sql   
SELECT ENAME, DEPTNO, SAL 
    -> FROM EMPLOYEE E
    -> WHERE SAL = ( SELECT MAX(SAL) FROM EMPLOYEE
    ->     WHERE DEPTNO = E.DEPTNO);
~~~
 Output
~~~SQL
+--------+--------+------+
| ENAME  | DEPTNO | SAL  |
+--------+--------+------+
| BLAKE  |     30 | 2850 |
| SCOTT  |     40 | 3000 |
| KING   |     20 | 5000 |
| MILLER |     10 | 1300 |
+--------+--------+------+
~~~
# 07. Display the names of employees who earn highest salaries in their respective job groups.
 Query
~~~sql   
[Aman]> SELECT ENAME, JOB, SAL
    -> FROM EMPLOYEE E
    -> WHERE SAL = ( SELECT MAX(SAL) FROM EMPLOYEE
    ->     WHERE JOB = E.JOB);
~~~
 Output
~~~SQL
+--------+-----------+------+
| ENAME  | JOB       | SAL  |
+--------+-----------+------+
| ALLEN  | SELESMAN  | 1600 |
| JONES  | MANAGER   | 2975 |
| SCOTT  | ANALYST   | 3000 |
| KING   | PRESIDENT | 5000 |
| FORD   | ANALYST   | 3000 |
| MILLER | CLERK     | 1300 |
+--------+-----------+------+

~~~
# 08. Display the employee names who are working in accounting dept.
 Query
~~~sql   
SELECT ENAME FROM EMPLOYEE
    -> WHERE DEPTNO = (SELECT DEPTNO FROM DEPARTMENT
    ->     WHERE DNAME = 'ACCOUNTING');
~~~
 Output
~~~SQL
+-------+
| ENAME |
+-------+
| SMITH |
| JONES |
| CLARK |
| KING  |
| ADAMS |
| FORD  |
+-------+
~~~
# 09. Display the employee names who are working in Mumbai.
 Query
~~~sql   
 SELECT ENAME FROM EMPLOYEE
    -> WHERE DEPTNO = ( SELECT DEPTNO FROM DEPARTMENT
    ->     WHERE LOCATION = 'MUMBAI');
~~~
 Output
~~~SQL
+--------+
| ENAME  |
+--------+
| MILLER |
+--------+
~~~
# 10. Display the job groups having total salary greater than the maximum salary for managers.
 Query
~~~sql   
SELECT JOB, SUM(SAL) AS TOTAL_SALARY
    -> FROM EMPLOYEE
    -> GROUP BY JOB
    -> HAVING SUM(SAL) > ( SELECT MAX(SAL) FROM EMPLOYEE 
    ->     WHERE JOB = 'MANAGER');
~~~
 Output
~~~SQL
+-----------+--------------+
| JOB       | TOTAL_SALARY |
+-----------+--------------+
| ANALYST   |         6000 |
| CLERK     |         4150 |
| MANAGER   |         8275 |
| PRESIDENT |         5000 |
| SELESMAN  |         5600 |
+-----------+--------------+
~~~
