# Experiment :- 3  

---
## (Advanced Data Retrieval using EMPLOYEE Table)

---

## 01. List all employees and jobs in Department 30 in descending order by salary

```sql
SELECT ENAME, JOB, SAL 
FROM EMPLOYEE
WHERE DEPTNO = 30
ORDER BY SAL DESC;

---------------------------------------
TABLE
SELECT ENAME, JOB, SAL FROM EMPLOYEE WHERE DEPTNO=30 ORDER BY SAL DESC;
```

```
+--------+----------+------+
| ENAME  | JOB      | SAL  |
+--------+----------+------+
| BLAKE  | MANAGER  | 2850 |
| ALLEN  | SALESMAN | 1600 |
| TURNER | SALESMAN | 1500 |
| MARTIN | SALESMAN | 1250 |
| WARD   | SALESMAN | 1250 |
| JAMES  | CLERK    | 950  |
+--------+----------+------+
```

---

## 02. List job and Department Number of employees whose name are five letters long begin with ‘A’ and end with ‘N’

```sql
SELECT JOB, DEPTNO 
FROM EMPLOYEE
WHERE ENAME LIKE 'A___N';

---------------------------------------
TABLE
SELECT JOB, DEPTNO FROM EMPLOYEE WHERE ENAME LIKE 'A___N';
```

```
+----------+--------+
| JOB      | DEPTNO |
+----------+--------+
| SALESMAN | 30     |
+----------+--------+
```

---

## 03. Display the name of employees whose name start with alphabet S

```sql
SELECT ENAME 
FROM EMPLOYEE
WHERE ENAME LIKE 'S%';

---------------------------------------
TABLE
SELECT ENAME FROM EMPLOYEE WHERE ENAME LIKE 'S%';
```

```
+--------+
| ENAME  |
+--------+
| SMITH  |
| SCOTT  |
+--------+
```

---

## 04. Display the names of employees whose name ends with alphabet S

```sql
SELECT ENAME 
FROM EMPLOYEE
WHERE ENAME LIKE '%S';

---------------------------------------
TABLE
SELECT ENAME FROM EMPLOYEE WHERE ENAME LIKE '%S';
```

```
+--------+
| ENAME  |
+--------+
| JONES  |
| ADAMS  |
| JAMES  |
+--------+
```

---

## 05. Display the names of employees working in department number 10 or 20 or 40 or employees working as clerks, salesman or analyst

```sql
SELECT ENAME 
FROM EMPLOYEE
WHERE DEPTNO IN (10,20,40)
OR JOB IN ('CLERK','SALESMAN','ANALYST');

---------------------------------------
TABLE
SELECT ENAME FROM EMPLOYEE WHERE DEPTNO IN(10,20,40) 
OR JOB IN('CLERK','SALESMAN','ANALYST');
```

```
+--------+
| ENAME  |
+--------+
| SMITH  |
| ALLEN  |
| WARD   |
| JONES  |
| MARTIN |
| SCOTT  |
| TURNER |
| ADAMS  |
| JAMES  |
| FORD   |
| MILLER |
| CLARK  |
| KING   |
+--------+
```

---

## 06. Display employee number and names for employees who earn commission

```sql
SELECT EMPNO, ENAME 
FROM EMPLOYEE
WHERE COMM IS NOT NULL;

---------------------------------------
TABLE
SELECT EMPNO, ENAME FROM EMPLOYEE WHERE COMM IS NOT NULL;
```

```
+-------+--------+
| EMPNO | ENAME  |
+-------+--------+
| 7499  | ALLEN  |
| 7521  | WARD   |
| 7654  | MARTIN |
| 7844  | TURNER |
+-------+--------+
```
---

## 07. Display employee number and total salary for each employee

```sql
SELECT EMPNO, (SAL + IFNULL(COMM,0)) AS TOTAL_SALARY
FROM EMPLOYEE;

---------------------------------------
TABLE
SELECT EMPNO, (SAL + IFNULL(COMM,0)) AS TOTAL_SALARY FROM EMPLOYEE;
```

```
+-------+--------------+
| EMPNO | TOTAL_SALARY |
+-------+--------------+
| 7369  | 800          |
| 7499  | 1900         |
| 7521  | 1550         |
| 7566  | 2975         |
| 7654  | 2650         |
| 7698  | 2850         |
| 7782  | 2450         |
| 7788  | 3000         |
| 7839  | 5000         |
| 7844  | 1500         |
| 7876  | 1100         |
| 7900  | 950          |
| 7902  | 3000         |
| 7934  | 1300         |
+-------+--------------+
```

---

## 08. Display employee number and annual salary for each employee

```sql
SELECT EMPNO, (SAL * 12) AS ANNUAL_SALARY
FROM EMPLOYEE;

---------------------------------------
TABLE
SELECT EMPNO, (SAL*12) AS ANNUAL_SALARY FROM EMPLOYEE;
```

```
+-------+---------------+
| EMPNO | ANNUAL_SALARY |
+-------+---------------+
| 7369  | 9600          |
| 7499  | 19200         |
| 7521  | 15000         |
| 7566  | 35700         |
| 7654  | 15000         |
| 7698  | 34200         |
| 7782  | 29400         |
| 7788  | 36000         |
| 7839  | 60000         |
| 7844  | 18000         |
| 7876  | 13200         |
| 7900  | 11400         |
| 7902  | 36000         |
| 7934  | 15600         |
+-------+---------------+
```

---

## 09. Display the names of all employees working as clerks and drawing a salary more than 3000

```sql
SELECT ENAME 
FROM EMPLOYEE
WHERE JOB = 'CLERK'
AND SAL > 3000;

---------------------------------------
TABLE
SELECT ENAME FROM EMPLOYEE WHERE JOB='CLERK' AND SAL>3000;
```

```
Empty Set
```

---

## 10. Display the names of employees who are working as clerk, salesman or analyst and drawing a salary more than 3000

```sql
SELECT ENAME 
FROM EMPLOYEE
WHERE JOB IN ('CLERK','SALESMAN','ANALYST')
AND SAL > 3000;

---------------------------------------
TABLE
SELECT ENAME FROM EMPLOYEE 
WHERE JOB IN('CLERK','SALESMAN','ANALYST') 
AND SAL>3000;
```

```
Empty Set
```

---


---

