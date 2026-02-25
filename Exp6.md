## Experiment -- 06

01 . Display EMPNO, ENAME, DEPTNO from employee table. Instead of displaying department numbers, display the related department name (Use DECODE function).
## Queries:
 ```sql
 SELECT EMPNO,
       ENAME,
       CASE DEPTNO
           WHEN 10 THEN 'RESEARCH'
           WHEN 20 THEN 'ACCOUNTING'
           WHEN 30 THEN 'SALES'
           WHEN 40 THEN 'OPERATIONS'
           ELSE 'UNKNOWN'
       END AS DNAME
FROM EMPLOYEE;
```
## Output:
```sql
+-------+--------+------------+
| EMPNO | ENAME  | DNAME      |
+-------+--------+------------+
|  7369 | SMITH  | ACCOUNTING |
|  7499 | ALLEN  | SALES      |
|  7521 | WARD   | SALES      |
|  7566 | JONES  | ACCOUNTING |
|  7654 | MARTIN | SALES      |
|  7698 | BLAKE  | SALES      |
|  7782 | CLARK  | ACCOUNTING |
|  7788 | SCOTT  | OPERATIONS |
|  7839 | KING   | ACCOUNTING |
|  7844 | TURNER | SALES      |
|  7876 | ADAMS  | ACCOUNTING |
|  7900 | JAMES  | SALES      |
|  7902 | FORD   | ACCOUNTING |
|  7934 | MILLER | RESEARCH   |
+-------+--------+------------+
```
02 . Display your age in days.
## Queries:
```sql
SELECT DATEDIFF(CURDATE(), '2007-03-16') AS AGE_IN_DAYS;
```
## Output:
```sql
+-------------+
| AGE_IN_DAYS |
+-------------+
|        6915 |
+-------------+
```
03 . Display your age in months.
## Queries:
```sql
SELECT TIMESTAMPDIFF(MONTH, '2007-03-16', CURDATE()) AS AGE_IN_MONTHS;
```
## Output:
```sql
+---------------+
| AGE_IN_MONTHS |
+---------------+
|           227 |
+---------------+
```
04 . Display the current date as 15th August Friday Nineteen Ninety-Seven.
## Queries:
```sql
SELECT DATE_FORMAT('1997-08-15', '%D %M %W ')
AS TODAYS_DATE;
```
## Output:
```sql
+--------------------------+
| TODAYS_DATE              |
+--------------------------+
|15th August Friday 1997   |
+--------------------------+
```
05 . Display the following output for each row from employee table.
Scott has joined the company on Wednesday 13th August Nineteen Ninety.
## Queries:
```sql
SELECT CONCAT(ENAME, 'HAS JOINED THE COMPANY ON',
  DATE_FORMAT(HIREDATE, '%W %D %M %Y')) AS EMPLOYEE_INFO
FROM EMPLOYEE;
```
## Output
```sql
+--------------------------------------------------------------+
| EMPLOYEE_INFO                                                |
+--------------------------------------------------------------+
| SMITH HAS JOINED THE COMPANY ON Wednesday 17th December 1980 |
| ALLEN HAS JOINED THE COMPANY ON Friday 20th February 1981    |
| WARD HAS JOINED THE COMPANY ON Sunday 22nd February 1981     |
| JONES HAS JOINED THE COMPANY ON Thursday 2nd April 1981      |
| MARTIN HAS JOINED THE COMPANY ON Monday 28th September 1981  |
| BLAKE HAS JOINED THE COMPANY ON Friday 1st May 1981          |
| CLARK HAS JOINED THE COMPANY ON Tuesday 9th June 1981        |
| SCOTT HAS JOINED THE COMPANY ON Thursday 9th December 1982   |
| KING HAS JOINED THE COMPANY ON Tuesday 17th November 1981    |
| TURNER HAS JOINED THE COMPANY ON Tuesday 8th September 1981  |
| ADAMS HAS JOINED THE COMPANY ON Wednesday 12th January 1983  |
| JAMES HAS JOINED THE COMPANY ON Thursday 3rd December 1981   |
| FORD HAS JOINED THE COMPANY ON Thursday 3rd December 1981    |
| MILLER HAS JOINED THE COMPANY ON Saturday 23rd January 1982  |
+--------------------------------------------------------------+
```
07 . Find the date for nearest Saturday after current date.
## Queries:
```sql
SELECT DATE_ADD(CURDATE(),
       INTERVAL (6 - WEEKDAY(CURDATE()) + 7) % 7 DAY) AS NEXT_SATURDAY;
```
## Output:
```sql
+---------------+
| NEXT_SATURDAY |
+---------------+
| 2026-02-14    |
+---------------+
```
08 . Display current time
## Queries:
```sql
SELECT CURTIME() AS CURRENTTIME;
```
## Output:
```sql
+-------------+
| CURRENTTIME |
+-------------+
| 14:23:28    |
+-------------+
```
09 . Display the date three months before the current date
## Queries:
```sql
SELECT DATE_SUB(CURDATE(), INTERVAL 3 MONTH) AS THREE_MONTHS_BEFORE;
```
## Output:
```sql
+---------------------+
| THREE_MONTHS_BEFORE |
+---------------------+
| 2025-11-14          |
+---------------------+
```
10 . Display those employees who joined in the company in the month of December
## Queries:
```sql
SELECT *
FROM EMPLOYEE
WHERE MONTH(HIREDATE) = 12;
```
## Output:
```sql
+-------+-------+---------+------+------------+------+------+--------+
| EMPNO | ENAME | JOB     | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+-------+---------+------+------------+------+------+--------+
|  7369 | SMITH | CLERK   | 7902 | 1980-12-17 |  968 | NULL |     20 |
|  7788 | SCOTT | ANALYST | 7566 | 1982-12-09 | 3630 | NULL |     40 |
|  7900 | JAMES | CLERK   | 7698 | 1981-12-03 | 1150 | NULL |     30 |
|  7902 | FORD  | ANALYST | 7566 | 1981-12-03 | 3630 | NULL |     20 |
+-------+-------+---------+------+------------+------+------+--------+
```
11 . Display those employees whose first 2 characters from hire date equal last 2 characters of salary
## Queries:
```sql
SELECT *
FROM EMPLOYEE
WHERE LPAD(DAY(HIREDATE),2,'0') = RIGHT(SAL,2);
```
## Output
```sql
Empty Set
```
12 . Display those employees whose 10% of salary is equal to the year of joining.
## Queries:
```sql
SELECT *
FROM EMPLOYEE
WHERE SAL * 0.10 = YEAR(HIREDATE);
```
## Output:
```sql
Empty set
```
13 . Display those employees who joined the company before 15 months
## Queries:
```sql
SELECT *
FROM EMPLOYEE
WHERE HIREDATE < DATE_SUB(CURDATE(), INTERVAL 15 MONTH);
```
## Output:
```sql
+-------+--------+-----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+-----------+------+------------+------+------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  968 | NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600 |  300 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250 |  300 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 3600 | NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250 | 1400 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 3449 | NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2965 | NULL |     20 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3630 | NULL |     40 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 6050 | NULL |     20 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1815 |    0 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1331 | NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 | 1150 | NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3630 | NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1573 | NULL |     10 |
+-------+--------+-----------+------+------------+------+------+--------+
```
14 .Display those employees who have joined before 15th of the month.
## Queries:
```sql
 SELECT *
FROM EMPLOYEE
WHERE DAY(HIREDATE) < 15;
```
## Output:
```sql
+-------+--------+----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB      | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+----------+------+------------+------+------+--------+
|  7566 | JONES  | MANAGER  | 7839 | 1981-04-02 | 3600 | NULL |     20 |
|  7698 | BLAKE  | MANAGER  | 7839 | 1981-05-01 | 3449 | NULL |     30 |
|  7782 | CLARK  | MANAGER  | 7839 | 1981-06-09 | 2965 | NULL |     20 |
|  7788 | SCOTT  | ANALYST  | 7566 | 1982-12-09 | 3630 | NULL |     40 |
|  7844 | TURNER | SALESMAN | 7698 | 1981-09-08 | 1815 |    0 |     30 |
|  7876 | ADAMS  | CLERK    | 7788 | 1983-01-12 | 1331 | NULL |     20 |
|  7900 | JAMES  | CLERK    | 7698 | 1981-12-03 | 1150 | NULL |     30 |
|  7902 | FORD   | ANALYST  | 7566 | 1981-12-03 | 3630 | NULL |     20 |
+-------+--------+----------+------+------------+------+------+--------+
```
15 . Display those employees whose joining date is available in DEPTNO
## Queries:
```sql
SELECT *
FROM EMPLOYEE
WHERE HIREDATE IS NOT NULL
AND DEPTNO IS NOT NULL;
```
## Output:
```sql
+-------+--------+-----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+-----------+------+------------+------+------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  968 | NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600 |  300 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250 |  300 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 3600 | NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250 | 1400 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 3449 | NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2965 | NULL |     20 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3630 | NULL |     40 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 6050 | NULL |     20 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1815 |    0 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1331 | NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 | 1150 | NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3630 | NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1573 | NULL |     10 |
+-------+--------+-----------+------+------------+------+------+--------+
```
