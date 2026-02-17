##Queries -- 5
01. Display the total number of employee working in the company
```sql
SELECT COUNT(*) FROM EMPLOYEE;

+----------+
| COUNT(*) |
+----------+
| 14       |
+----------+
```
02. Display the total salary being paid to all employees
```sql
SELECT SUM(SAL) FROM EMPLOYEE;

+----------+
| SUM(SAL) |
+----------+
| 29025    |
+----------+
```
03. Display the maximum salary from employee table
```sql
SELECT MAX(SAL) FROM EMPLOYEE;

+----------+
| MAX(SAL) |
+----------+
| 5000     |
+----------+
```
04. Display the minimum salary from employee table
```sql
SELECT MIN(SAL) FROM EMPLOYEE;

+----------+
| MIN(SAL) |
+----------+
| 800      |
+----------+
```
05. Display the average salary from employee table
```sql
SELECT AVG(SAL) FROM EMPLOYEE;

+-----------+
| AVG(SAL)  |
+-----------+
| 2073.2143 |
+-----------+
```
06. Display the maximum salary being paid to clerk
```sql
SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB='CLERK';

+----------+
| MAX(SAL) |
+----------+
| 1300     |
+----------+
```
07. Display the maximum salary being paid in dept no 20
```sql
SELECT MAX(SAL) FROM EMPLOYEE WHERE DEPTNO=20;

+----------+
| MAX(SAL) |
+----------+
| 3000     |
+----------+
```
08. Display the minimum salary paid to any salesman
```sql
SELECT MIN(SAL) FROM EMPLOYEE WHERE JOB='SALESMAN';

+----------+
| MIN(SAL) |
+----------+
| 1250     |
+----------+
```
09. Display the average salary drawn by managers
```sql
SELECT AVG(SAL) FROM EMPLOYEE WHERE JOB='MANAGER';

+----------+
| AVG(SAL) |
+----------+
| 2750     |
+----------+
```
10. Display the total salary drawn by analyst working in dept no 40
```sql
SELECT SUM(SAL) FROM EMPLOYEE WHERE JOB='ANALYST' AND DEPTNO=40;

+----------+
| SUM(SAL) |
+----------+
| NULL     |
+----------+
```
11. Display the names of the employee in Uppercase
```sql
SELECT UPPER(ENAME) FROM EMPLOYEE;

+---------------+
| UPPER(ENAME)  |
+---------------+
| SMITH         |
| ALLEN         |
| WARD          |
| JONES         |
| MARTIN        |
| BLAKE         |
| CLARK         |
| SCOTT         |
| KING          |
| TURNER        |
| ADAMS         |
| JAMES         |
| FORD          |
| MILLER        |
+---------------+
```
12. Display the names of the employee in Lowercase
```sql
SELECT LOWER(ENAME) FROM EMPLOYEE;

+---------------+
| LOWER(ENAME)  |
+---------------+
| smith         |
| allen         |
| ward          |
| jones         |
| martin        |
| blake         |
| clark         |
| scott         |
| king          |
| turner        |
| adams         |
| james         |
| ford          |
| miller        |
+---------------+
```
13. Display the names of the employee in Proper case
```sql
SELECT CONCAT(UCASE(LEFT(ENAME,1)),LCASE(SUBSTRING(ENAME,2))) FROM EMPLOYEE;

+-----------------------------------------------+
| CONCAT(UCASE(LEFT(ENAME,1)),LCASE(SUBSTRING(ENAME,2))) |
+-----------------------------------------------+
| Smith                                         |
| Allen                                         |
| Ward                                          |
| Jones                                         |
| Martin                                        |
| Blake                                         |
| Clark                                         |
| Scott                                         |
| King                                          |
| Turner                                        |
| Adams                                         |
| James                                         |
| Ford                                          |
| Miller                                        |
+-----------------------------------------------+
```
14. Display the length of your name using appropriate function
```sql
SELECT LENGTH('OMIKA');

+------------------+
| LENGTH('OMIKA')  |
+------------------+
| 5                |
+------------------+
```
15. Display the length of all the employee names
```sql
SELECT ENAME, LENGTH(ENAME) FROM EMPLOYEE;

+--------+---------------+
| ENAME  | LENGTH(ENAME) |
+--------+---------------+
| SMITH  | 5             |
| ALLEN  | 5             |
| WARD   | 4             |
| JONES  | 5             |
| MARTIN | 6             |
| BLAKE  | 5             |
| CLARK  | 5             |
| SCOTT  | 5             |
| KING   | 4             |
| TURNER | 6             |
| ADAMS  | 5             |
| JAMES  | 5             |
| FORD   | 4             |
| MILLER | 6             |
+--------+---------------+
```
