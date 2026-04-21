# EXPERIMENT-8
# 01. Display all employees with their dept name.
 Query
~~~sql   
 SELECT e.ename, d.dname
    -> FROM employee e
    -> JOIN department d
    -> ON e.deptno = d.deptno;
~~~
 Output
~~~SQL
+--------+------------+
| ename  | dname      |
+--------+------------+
| MILLER | RESEARCH   |
| SMITH  | ACCOUNTING |
| JONES  | ACCOUNTING |
| CLARK  | ACCOUNTING |
| KING   | ACCOUNTING |
| ADAMS  | ACCOUNTING |
| FORD   | ACCOUNTING |
| ALLEN  | SALES      |
| WARD   | SALES      |
| MARTIN | SALES      |
| BLAKE  | SALES      |
| TURNER | SALES      |
| JAMES  | SALES      |
| SCOTT  | OPERATIONS |
+--------+------------+
~~~
# 02. Display those employees whose manager names is jones, and also display their manager name.
 Query
~~~sql   
 SELECT e.ename AS employee_name, m.ename AS manager_name
    -> FROM employee e
    -> JOIN employee m
    -> ON e.mgr = m.empno
    -> WHERE m.ename = 'JONES';
~~~
 Output
~~~SQL
+---------------+--------------+
| employee_name | manager_name |
+---------------+--------------+
| SCOTT         | JONES        |
| FORD          | JONES        |
+---------------+--------------+
~~~
# 03. Display employee name, his job, his dept name, his manager name, his grade and make out of an under department wise.
 Query
~~~sql   
SELECT e.ename, e.job, d.dname, m.ename AS Manager ,s.grade
    -> FROM employee e
    -> JOIN department d ON e.deptno = d.deptno
    -> LEFT JOIN employee m ON e.mgr = m.empno
    -> JOIN salgrade s ON e.sal BETWEEN s.losal AND s.hisal
    -> ORDER BY d.dname;

~~~
 Output
~~~SQL
+--------+-----------+------------+---------+-------+
| ename  | job       | dname      | Manager | grade |
+--------+-----------+------------+---------+-------+
| SMITH  | CLERK     | ACCOUNTING | FORD    | A     |
| CLARK  | MANAGER   | ACCOUNTING | KING    | D     |
| KING   | PRESIDENT | ACCOUNTING | NULL    | E     |
| JONES  | MANAGER   | ACCOUNTING | KING    | D     |
| ADAMS  | CLERK     | ACCOUNTING | SCOTT   | A     |
| FORD   | ANALYST   | ACCOUNTING | JONES   | D     |
| SCOTT  | ANALYST   | OPERATIONS | JONES   | D     |
| MILLER | CLERK     | RESEARCH   | CLARK   | B     |
| WARD   | SELESMAN  | SALES      | BLAKE   | B     |
| TURNER | SELESMAN  | SALES      | BLAKE   | C     |
| JAMES  | CLERK     | SALES      | BLAKE   | A     |
| BLAKE  | MANAGER   | SALES      | KING    | D     |
| ALLEN  | SELESMAN  | SALES      | BLAKE   | C     |
| MARTIN | SELESMAN  | SALES      | BLAKE   | B     |
+--------+-----------+------------+---------+-------+

~~~
# 04. List out all the employees name, job, and salary grade and department name for everyone in the company except ‘clerk’. Sort on salary display the highest salary.
 Query
~~~sql   
SELECT e.ename, e.job, e.sal, s.grade , d.dname
    -> FROM employee e
    -> JOIN department d ON e.deptno = d.deptno
    -> JOIN salgrade s ON e.sal BETWEEN s.losal AND s.hisal
    -> WHERE e.job != 'CLERK'
    -> ORDER BY e.sal DESC;
~~~
 Output
~~~SQL
+--------+-----------+------+-------+------------+
| ename  | job       | sal  | grade | dname      |
+--------+-----------+------+-------+------------+
| KING   | PRESIDENT | 5000 | E     | ACCOUNTING |
| SCOTT  | ANALYST   | 3000 | D     | OPERATIONS |
| FORD   | ANALYST   | 3000 | D     | ACCOUNTING |
| JONES  | MANAGER   | 2975 | D     | ACCOUNTING |
| BLAKE  | MANAGER   | 2850 | D     | SALES      |
| CLARK  | MANAGER   | 2450 | D     | ACCOUNTING |
| ALLEN  | SELESMAN  | 1600 | C     | SALES      |
| TURNER | SELESMAN  | 1500 | C     | SALES      |
| WARD   | SELESMAN  | 1250 | B     | SALES      |
| MARTIN | SELESMAN  | 1250 | B     | SALES      |
+--------+-----------+------+-------+------------+
~~~
# 05. Display employee name, his job and his manager. Display also employees who are without manager.
 Query
~~~sql   
 SELECT e.ename, e.job, IFNULL(m.ename, 'NO MANAGER') AS Manager 
    -> FROM employee e 
    -> LEFT JOIN employee m ON e.mgr = m.empno;
~~~
 Output
~~~SQL
+--------+-----------+------------+
| ename  | job       | Manager    |
+--------+-----------+------------+
| SMITH  | CLERK     | FORD       |
| ALLEN  | SELESMAN  | BLAKE      |
| WARD   | SELESMAN  | BLAKE      |
| JONES  | MANAGER   | KING       |
| MARTIN | SELESMAN  | BLAKE      |
| BLAKE  | MANAGER   | KING       |
| CLARK  | MANAGER   | KING       |
| SCOTT  | ANALYST   | JONES      |
| KING   | PRESIDENT | NO MANAGER |
| TURNER | SELESMAN  | BLAKE      |
| ADAMS  | CLERK     | SCOTT      |
| JAMES  | CLERK     | BLAKE      |
| FORD   | ANALYST   | JONES      |
| MILLER | CLERK     | CLARK      |
+--------+-----------+------------+

~~~
# 06. List the employee name, job, annual salary, deptno, dept name and grade who earn 36000 a year or who are not clerks.
 Query
~~~sql   
SELECT e.ename, e.job, (e.sal * 12) AS Annual_Salary, e.deptno, d.dname, s.grade
    -> FROM employee e
    -> JOIN department d
    -> ON e.deptno = d.deptno
    -> JOIN salgrade s ON e.sal BETWEEN s.losal AND s.hisal
    -> WHERE (e.sal * 12) = 36000 OR e.job <> 'CLERK';
~~~
 Output
~~~SQL
+--------+-----------+---------------+--------+------------+-------+
| ename  | job       | Annual_Salary | deptno | dname      | grade |
+--------+-----------+---------------+--------+------------+-------+
| WARD   | SELESMAN  |         15000 |     30 | SALES      | B     |
| MARTIN | SELESMAN  |         15000 |     30 | SALES      | B     |
| ALLEN  | SELESMAN  |         19200 |     30 | SALES      | C     |
| TURNER | SELESMAN  |         18000 |     30 | SALES      | C     |
| JONES  | MANAGER   |         35700 |     20 | ACCOUNTING | D     |
| CLARK  | MANAGER   |         29400 |     20 | ACCOUNTING | D     |
| FORD   | ANALYST   |         36000 |     20 | ACCOUNTING | D     |
| BLAKE  | MANAGER   |         34200 |     30 | SALES      | D     |
| SCOTT  | ANALYST   |         36000 |     40 | OPERATIONS | D     |
| KING   | PRESIDENT |         60000 |     20 | ACCOUNTING | E     |
+--------+-----------+---------------+--------+------------+-------+

~~~
# 07. List ename, job, annual sal, deptno, dname and grade who earn 30000 per year and who are not clerks.
 Query
~~~sql   
SELECT e.ename, e.job, (e.sal * 12) AS Annual_Salary,e.deptno, d.dname, s.grade
    -> FROM employee e 
    -> JOIN department d ON e.deptno = d.deptno 
    -> JOIN salgrade s ON e.sal BETWEEN s.losal AND s.hisal
    -> WHERE (e.sal * 12) = 30000 AND e.job <> 'CLERK';
~~~
 Output
~~~SQL
Empty set (0.004 sec)
~~~
# 08. List out all employees by name and number along with their manager’s name and number also display ‘no manager’ who has no manager.
 Query
~~~sql   
SELECT e.empno, e.ename, IFNULL(m.empno, 'NULL') AS Manager_No, IFNULL(m.ename, 'NO MANAGER') AS Manager_Name 
    -> FROM employee e 
    -> LEFT JOIN employee m ON e.mgr = m.empno;
~~~
 Output
~~~SQL
+-------+--------+------------+--------------+
| empno | ename  | Manager_No | Manager_Name |
+-------+--------+------------+--------------+
|  7369 | SMITH  | 7902       | FORD         |
|  7499 | ALLEN  | 7698       | BLAKE        |
|  7521 | WARD   | 7698       | BLAKE        |
|  7566 | JONES  | 7839       | KING         |
|  7654 | MARTIN | 7698       | BLAKE        |
|  7698 | BLAKE  | 7839       | KING         |
|  7782 | CLARK  | 7839       | KING         |
|  7788 | SCOTT  | 7566       | JONES        |
|  7839 | KING   | NULL       | NO MANAGER   |
|  7844 | TURNER | 7698       | BLAKE        |
|  7876 | ADAMS  | 7788       | SCOTT        |
|  7900 | JAMES  | 7698       | BLAKE        |
|  7902 | FORD   | 7566       | JONES        |
|  7934 | MILLER | 7782       | CLARK        |
+-------+--------+------------+--------------+
~~~
# 09. Select dept name, dept no and sum of sal
 Query
~~~sql   
SELECT d.deptno, e.deptno, SUM(e.sal) 
    -> FROM employee e 
    -> JOIN department d ON e.deptno = d.deptno 
    -> GROUP BY e.deptno, d.dname;
~~~
 Output
~~~SQL
+--------+--------+------------+
| deptno | deptno | SUM(e.sal) |
+--------+--------+------------+
|     10 |     10 |       1300 |
|     20 |     20 |      15325 |
|     30 |     30 |       9400 |
|     40 |     40 |       3000 |
+--------+--------+------------+
~~~
# 10. Display employee number, name and location of the department in which he is working
 Query
~~~sql   
SELECT e.empno, e.ename, d.location
    -> FROM employee e
    -> JOIN department d ON e.deptno = d.deptno;
~~~
 Output
~~~SQL
+-------+--------+-----------+
| empno | ename  | location  |
+-------+--------+-----------+
|  7934 | MILLER | MUMBAI    |
|  7369 | SMITH  | CHENNAI   |
|  7566 | JONES  | CHENNAI   |
|  7782 | CLARK  | CHENNAI   |
|  7839 | KING   | CHENNAI   |
|  7876 | ADAMS  | CHENNAI   |
|  7902 | FORD   | CHENNAI   |
|  7499 | ALLEN  | HYDERABAD |
|  7521 | WARD   | HYDERABAD |
|  7654 | MARTIN | HYDERABAD |
|  7698 | BLAKE  | HYDERABAD |
|  7844 | TURNER | HYDERABAD |
|  7900 | JAMES  | HYDERABAD |
|  7788 | SCOTT  | DELHI     |
+-------+--------+-----------+

~~~
# 11. Display employee name and department name for each employee.
 Query
~~~sql   
SELECT e.ename, d.dname FROM employee e JOIN department d ON e.deptno = d.deptno;
~~~
 Output
~~~SQL
+--------+------------+
| ename  | dname      |
+--------+------------+
| MILLER | RESEARCH   |
| SMITH  | ACCOUNTING |
| JONES  | ACCOUNTING |
| CLARK  | ACCOUNTING |
| KING   | ACCOUNTING |
| ADAMS  | ACCOUNTING |
| FORD   | ACCOUNTING |
| ALLEN  | SALES      |
| WARD   | SALES      |
| MARTIN | SALES      |
| BLAKE  | SALES      |
| TURNER | SALES      |
| JAMES  | SALES      |
| SCOTT  | OPERATIONS |
+--------+------------+

~~~
