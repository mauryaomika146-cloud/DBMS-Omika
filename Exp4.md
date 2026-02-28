## QUERIES -- 4
01 . Display employees who joined before 30-Jun-1980 or after 31-Dec-1981
```sql
 SELECT*FROM EMPLOYEE
WHERE HIREDATE < '1980-06-30'
    OR HIREDATE > '1981-12-31';
    -----------------------------------------
+-------+--------+---------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB     | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+---------+------+------------+------+------+--------+
|  7788 | SCOTT  | ANALYST | 7566 | 1982-12-09 | 3000 | NULL |     40 |
|  7876 | ADAMS  | CLERK   | 7788 | 1983-01-12 | 1100 | NULL |     20 |
|  7934 | MILLER | CLERK   | 7782 | 1982-01-23 | 1300 | NULL |     10 |
+-------+--------+---------+------+------------+------+------+--------+
```
02 . Display names of employees whose second alphabet is ‘A’
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE ENAME LIKE '_A%';
--------------------------------------------------+--------+
| ENAME  |
+--------+
| WARD   |
| MARTIN |
| JAMES  |
+--------+
```
03 . Display names of employees whose name is exactly five characters long
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE LENGTH(ENAME) = 5;
----------------------------------------------------
+-------+
| ENAME |
+-------+
| SMITH |
| ALLEN |
| JONES |
| BLAKE |
| CLARK |
| SCOTT |
| ADAMS |
| JAMES |
+-------+
```
04 . Display names of employees whose second last alphabet is ‘E’
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE ENAME LIKE '%E_';
---------------------------------------------------
+--------+
| ENAME  |
+--------+
| ALLEN  |
| JONES  |
| TURNER |
| JAMES  |
| MILLER |
+--------+
```
05 . Display names of employees who are NOT working as salesman, clerk or analyst
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB NOT IN ('SALESMAN', 'CLERK', 'ANALYST');
------------------------------------------------------
+-------+
| ENAME |
+-------+
| JONES |
| BLAKE |
| CLARK |
| KING  |
+-------+
```
06 . Display employee name and annual salary (SAL × 12), highest salary first
```sql
SELECT ENAME, (SAL * 12) AS ANNUAL_SALARY
FROM EMPLOYEE
ORDER BY ANNUAL_SALARY DESC;
--------------------------------------------
+--------+---------------+
| ENAME  | ANNUAL_SALARY |
+--------+---------------+
| KING   |         60000 |
| SCOTT  |         36000 |
| FORD   |         36000 |
| JONES  |         35700 |
| BLAKE  |         34200 |
| CLARK  |         29400 |
| ALLEN  |         19200 |
| TURNER |         18000 |
| MILLER |         15600 |
| MARTIN |         15000 |
| WARD   |         15000 |
| ADAMS  |         13200 |
| JAMES  |         11400 |
| SMITH  |          9600 |
+--------+---------------+
```
07 . Display name, SAL, HRA, DA, PF and TOTAL SALARY
HRA = 15% of SAL
DA = 10% of SAL
PF = 5% of SAL
TOTAL SALARY = (SAL + HRA + DA) − PF
```sql
SELECT 
    ENAME,
    SAL,
    (SAL * 0.15) AS HRA,
    (SAL * 0.10) AS DA,
    (SAL * 0.05) AS PF,
    (SAL + (SAL * 0.15) + (SAL * 0.10) - (SAL * 0.05)) AS TOTALSAL
FROM EMPLOYEE
ORDER BY TOTALSAL;
--------------------------------------------------------+--------+------+--------+--------+--------+----------+
| ENAME  | SAL  | HRA    | DA     | PF     | TOTALSAL |
+--------+------+--------+--------+--------+----------+
| SMITH  |  800 | 120.00 |  80.00 |  40.00 |   960.00 |
| JAMES  |  950 | 142.50 |  95.00 |  47.50 |  1140.00 |
| ADAMS  | 1100 | 165.00 | 110.00 |  55.00 |  1320.00 |
| WARD   | 1250 | 187.50 | 125.00 |  62.50 |  1500.00 |
| MARTIN | 1250 | 187.50 | 125.00 |  62.50 |  1500.00 |
| MILLER | 1300 | 195.00 | 130.00 |  65.00 |  1560.00 |
| TURNER | 1500 | 225.00 | 150.00 |  75.00 |  1800.00 |
| ALLEN  | 1600 | 240.00 | 160.00 |  80.00 |  1920.00 |
| CLARK  | 2450 | 367.50 | 245.00 | 122.50 |  2940.00 |
| BLAKE  | 2850 | 427.50 | 285.00 | 142.50 |  3420.00 |
| JONES  | 2975 | 446.25 | 297.50 | 148.75 |  3570.00 |
| FORD   | 3000 | 450.00 | 300.00 | 150.00 |  3600.00 |
| SCOTT  | 3000 | 450.00 | 300.00 | 150.00 |  3600.00 |
| KING   | 5000 | 750.00 | 500.00 | 250.00 |  6000.00 |
+--------+------+--------+--------+--------+----------+
```
08 . Update salary by 10% for employees NOT eligible for commission
```sql
UPDATE EMPLOYEE
SET SAL = SAL * 1.10
WHERE COMM IS NULL OR COMM = 0;
SELECT ENAME,SAL,COMM
FROM EMPLOYEE;
----------------------------------------------------+--------+------+------+
| ENAME  | SAL  | COMM |
+--------+------+------+
| SMITH  |  968 | NULL |
| ALLEN  | 1600 |  300 |
| WARD   | 1250 |  300 |
| JONES  | 3600 | NULL |
| MARTIN | 1250 | 1400 |
| BLAKE  | 3449 | NULL |
| CLARK  | 2965 | NULL |
| SCOTT  | 3630 | NULL |
| KING   | 6050 | NULL |
| TURNER | 1815 |    0 |
| ADAMS  | 1331 | NULL |
| JAMES  | 1150 | NULL |
| FORD   | 3630 | NULL |
| MILLER | 1573 | NULL |
+--------+------+------+
```
09 . Display employees whose salary is more than 3000 after 20% increment
```sql
SELECT ENAME, SAL, (SAL * 1.20) AS UPDATED_SALARY
FROM EMPLOYEE
WHERE (SAL * 1.20) > 3000;
------------------------------------------------+-------+------+----------------+
| ENAME | SAL  | UPDATED_SALARY |
+-------+------+----------------+
| JONES | 3600 |        4320.00 |
| BLAKE | 3449 |        4138.80 |
| CLARK | 2965 |        3558.00 |
| SCOTT | 3630 |        4356.00 |
| KING  | 6050 |        7260.00 |
| FORD  | 3630 |        4356.00 |
+-------+------+----------------+
```
10 . Display employees whose salary contains at least 3 digits
```sql
SELECT ENAME, SAL
FROM EMPLOYEE
WHERE SAL >= 100;
---------------------------
+--------+------+
| ENAME  | SAL  |
+--------+------+
| SMITH  |  968 |
| ALLEN  | 1600 |
| WARD   | 1250 |
| JONES  | 3600 |
| MARTIN | 1250 |
| BLAKE  | 3449 |
| CLARK  | 2965 |
| SCOTT  | 3630 |
| KING   | 6050 |
| TURNER | 1815 |
| ADAMS  | 1331 |
| JAMES  | 1150 |
| FORD   | 3630 |
| MILLER | 1573 |
+--------+------+
```
