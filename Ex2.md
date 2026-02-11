# PRACTICAL FILE ASSIGNMENT – QUESTION 2  
## (Retrieving Data using EMPLOYEE Table)

---

## 01. List all distinct jobs in Employee

```sql
SELECT DISTINCT JOB FROM EMPLOYEE;

---------------------------------------
TABLE
SELECT DISTINCT JOB FROM EMPLOYEE;
```

```
+-----------+
| JOB       |
+-----------+
| CLERK     |
| SALESMAN  |
| MANAGER   |
| ANALYST   |
| PRESIDENT |
+-----------+
```

---

## 02. List all information about employee in Department Number 30

```sql
SELECT * FROM EMPLOYEE
WHERE DEPTNO = 30;

---------------------------------------
TABLE
SELECT * FROM EMPLOYEE WHERE DEPTNO = 30;
```

```
+-------+--------+----------+------+------------+------+-------+--------+
| EMPNO | ENAME  | JOB      | MGR  | HIREDATE   | SAL  | COMM  | DEPTNO |
+-------+--------+----------+------+------------+------+-------+--------+
| 7499  | ALLEN  | SALESMAN | 7698 | 1981-02-20 | 1600 | 300   | 30     |
| 7521  | WARD   | SALESMAN | 7698 | 1981-02-22 | 1250 | 300   | 30     |
| 7654  | MARTIN | SALESMAN | 7698 | 1981-09-28 | 1250 | 1400  | 30     |
| 7698  | BLAKE  | MANAGER  | 7839 | 1981-05-01 | 2850 | NULL  | 30     |
| 7844  | TURNER | SALESMAN | 7698 | 1981-09-08 | 1500 | 0     | 30     |
| 7900  | JAMES  | CLERK    | 7698 | 1981-12-03 | 950  | NULL  | 30     |
+-------+--------+----------+------+------------+------+-------+--------+
```

---

## 03. Find all department numbers with department names greater than 20

```sql
SELECT DEPTNO, DNAME FROM DEPARTMENT
WHERE DEPTNO > 20;

---------------------------------------
TABLE
SELECT DEPTNO, DNAME FROM DEPARTMENT WHERE DEPTNO > 20;
```

```
+--------+------------+
| DEPTNO | DNAME      |
+--------+------------+
| 30     | SALES      |
| 40     | OPERATIONS |
+--------+------------+
```

---

## 04. Find all information about all the managers as well as clerks in department 30

```sql
SELECT * FROM EMPLOYEE
WHERE DEPTNO = 30
AND (JOB = 'MANAGER' OR JOB = 'CLERK');

---------------------------------------
TABLE
SELECT * FROM EMPLOYEE WHERE DEPTNO=30 AND (JOB='MANAGER' OR JOB='CLERK');
```

```
+-------+--------+----------+------+------------+------+-------+--------+
| EMPNO | ENAME  | JOB      | MGR  | HIREDATE   | SAL  | COMM  | DEPTNO |
+-------+--------+----------+------+------------+------+-------+--------+
| 7698  | BLAKE  | MANAGER  | 7839 | 1981-05-01 | 2850 | NULL  | 30     |
| 7900  | JAMES  | CLERK    | 7698 | 1981-12-03 | 950  | NULL  | 30     |
+-------+--------+----------+------+------------+------+-------+--------+
```

---

## 05. List the Employee name, Employee numbers and department of all clerks

```sql
SELECT ENAME, EMPNO, DEPTNO FROM EMPLOYEE
WHERE JOB = 'CLERK';

---------------------------------------
TABLE
SELECT ENAME, EMPNO, DEPTNO FROM EMPLOYEE WHERE JOB='CLERK';
```

```
+--------+-------+--------+
| ENAME  | EMPNO | DEPTNO |
+--------+-------+--------+
| SMITH  | 7369  | 20     |
| ADAMS  | 7876  | 20     |
| JAMES  | 7900  | 30     |
| MILLER | 7934  | 10     |
+--------+-------+--------+
```

---

## 06. Find all managers not in department 30

```sql
SELECT * FROM EMPLOYEE
WHERE JOB = 'MANAGER'
AND DEPTNO <> 30;

---------------------------------------
TABLE
SELECT * FROM EMPLOYEE WHERE JOB='MANAGER' AND DEPTNO<>30;
```

```
+-------+-------+---------+------+------------+------+-------+--------+
| EMPNO | ENAME | JOB     | MGR  | HIREDATE   | SAL  | COMM  | DEPTNO |
+-------+-------+---------+------+------------+------+-------+--------+
| 7566  | JONES | MANAGER | 7839 | 1981-04-02 | 2975 | NULL  | 20     |
| 7782  | CLARK | MANAGER | 7839 | 1981-06-09 | 2450 | NULL  | 20     |
+-------+-------+---------+------+------------+------+-------+--------+
```

---

## 07. List information about all Employees in department 10 who are not manager or clerks

```sql
SELECT * FROM EMPLOYEE
WHERE DEPTNO = 10
AND JOB NOT IN ('MANAGER','CLERK');

---------------------------------------
TABLE
SELECT * FROM EMPLOYEE WHERE DEPTNO=10 AND JOB NOT IN('MANAGER','CLERK');
```

```
Empty Set
```

---

## 08. Find Employees and jobs earning between 1200 and 1400

```sql
SELECT ENAME, JOB FROM EMPLOYEE
WHERE SAL BETWEEN 1200 AND 1400;

---------------------------------------
TABLE
SELECT ENAME, JOB FROM EMPLOYEE WHERE SAL BETWEEN 1200 AND 1400;
```

```
+--------+----------+
| ENAME  | JOB      |
+--------+----------+
| WARD   | SALESMAN |
| MARTIN | SALESMAN |
| MILLER | CLERK    |
+--------+----------+
```

---

## 09. List Name and Department Number of employee who are clerks, analyst or salesman

```sql
SELECT ENAME, DEPTNO FROM EMPLOYEE
WHERE JOB IN ('CLERK','ANALYST','SALESMAN');

---------------------------------------
TABLE
SELECT ENAME, DEPTNO FROM EMPLOYEE WHERE JOB IN('CLERK','ANALYST','SALESMAN');
```

```
+--------+--------+
| ENAME  | DEPTNO |
+--------+--------+
| SMITH  | 20     |
| ALLEN  | 30     |
| WARD   | 30     |
| MARTIN | 30     |
| SCOTT  | 40     |
| TURNER | 30     |
| ADAMS  | 20     |
| JAMES  | 30     |
| FORD   | 20     |
| MILLER | 10     |
+--------+--------+
```

---

## 10. List Name and Department Number of employee whose names begin with M

```sql
SELECT ENAME, DEPTNO FROM EMPLOYEE
WHERE ENAME LIKE 'M%';

---------------------------------------
TABLE
SELECT ENAME, DEPTNO FROM EMPLOYEE WHERE ENAME LIKE 'M%';
```

```
+--------+--------+
| ENAME  | DEPTNO |
+--------+--------+
| MARTIN | 30     |
| MILLER | 10     |
+--------+--------+
```

