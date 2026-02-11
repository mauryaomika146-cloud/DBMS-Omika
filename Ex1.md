# EXPERIMENT :- 01

---

## CREATING DATABASE

```sql
CREATE DATABASE OMIKA;
USE OMIKA;
```

---

## CREATING TABLE DEPARTMENT

```sql
CREATE TABLE DEPARTMENT (
    DEPTNO INT(2) PRIMARY KEY,
    DNAME VARCHAR(15) NOT NULL
);
```

---

## INSERT VALUES IN DEPARTMENT

```sql
INSERT INTO DEPARTMENT VALUES
(10,'RESEARCH'),
(20,'ACCOUNTING'),
(30,'SALES'),
(40,'OPERATIONS');
```

---

## VIEW TABLE DEPARTMENT

```sql
SELECT * FROM DEPARTMENT;
```

### OUTPUT:

```
+--------+-------------+
| DEPTNO | DNAME       |
+--------+-------------+
| 10     | RESEARCH    |
| 20     | ACCOUNTING  |
| 30     | SALES       |
| 40     | OPERATIONS  |
+--------+-------------+
```

---

## CREATING TABLE EMPLOYEE

```sql
CREATE TABLE EMPLOYEE (
    EMPNO INT(4) PRIMARY KEY,
    ENAME VARCHAR(20) NOT NULL,
    JOB VARCHAR(20),
    MGR INT(4),
    HIREDATE DATE,
    SAL INT(10),
    COMM INT(7),
    DEPTNO INT(2),
    FOREIGN KEY (DEPTNO) REFERENCES DEPARTMENT(DEPTNO)
);
```

---

## INSERT VALUES IN EMPLOYEE

```sql
INSERT INTO EMPLOYEE VALUES
(7369,'SMITH','CLERK',7902,'1980-12-17',800,NULL,20),
(7499,'ALLEN','SALESMAN',7698,'1981-02-20',1600,300,30),
(7521,'WARD','SALESMAN',7698,'1981-02-22',1250,300,30),
(7566,'JONES','MANAGER',7839,'1981-04-02',2975,NULL,20),
(7654,'MARTIN','SALESMAN',7698,'1981-09-28',1250,1400,30),
(7698,'BLAKE','MANAGER',7839,'1981-05-01',2850,NULL,30),
(7782,'CLARK','MANAGER',7839,'1981-06-09',2450,NULL,20),
(7788,'SCOTT','ANALYST',7566,'1982-12-09',3000,NULL,40),
(7839,'KING','PRESIDENT',NULL,'1981-11-17',5000,NULL,20),
(7844,'TURNER','SALESMAN',7698,'1981-09-08',1500,0,30),
(7876,'ADAMS','CLERK',7788,'1983-01-12',1100,NULL,20),
(7900,'JAMES','CLERK',7698,'1981-12-03',950,NULL,30),
(7902,'FORD','ANALYST',7566,'1981-12-03',3000,NULL,20);
```

---

## VIEW TABLE EMPLOYEE

```sql
SELECT EMPNO, ENAME, JOB, SAL, DEPTNO FROM EMPLOYEE;
```

### OUTPUT:

```
+-------+--------+-----------+------+--------+
| EMPNO | ENAME  | JOB       | SAL  | DEPTNO|
+-------+--------+-----------+------+--------+
| 7369  | SMITH  | CLERK     | 800  | 20    |
| 7499  | ALLEN  | SALESMAN  | 1600 | 30    |
| 7521  | WARD   | SALESMAN  | 1250 | 30    |
| 7566  | JONES  | MANAGER   | 2975 | 20    |
| 7654  | MARTIN | SALESMAN  | 1250 | 30    |
| 7698  | BLAKE  | MANAGER   | 2850 | 30    |
| 7782  | CLARK  | MANAGER   | 2450 | 20    |
| 7788  | SCOTT  | ANALYST   | 3000 | 40    |
| 7839  | KING   | PRESIDENT | 5000 | 20    |
| 7844  | TURNER | SALESMAN  | 1500 | 30    |
| 7876  | ADAMS  | CLERK     | 1100 | 20    |
| 7900  | JAMES  | CLERK     | 950  | 30    |
| 7902  | FORD   | ANALYST   | 3000 | 20    |
+-------+--------+-----------+------+--------+
```

---

# QUERIES

---

## 1. Create EMPLOYEE_MASTER

```sql
CREATE TABLE EMPLOYEE_MASTER AS
SELECT * FROM EMPLOYEE;
```

---
## 02. Delete employees where DEPTNO = 10

```sql
DELETE FROM EMPLOYEE_MASTER
WHERE DEPTNO = 10;

---------------------------------------
TABLE
SELECT * FROM EMPLOYEE_MASTER;
```

```
+-------+--------+-----------+------+------------+------+-------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL  | COMM  | DEPTNO |
+-------+--------+-----------+------+------------+------+-------+--------+
| 7369  | SMITH  | CLERK     | 7902 | 1980-12-17 | 800  | NULL  | 20     |
| 7499  | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600 | 300   | 30     |
| 7521  | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250 | 300   | 30     |
| 7566  | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975 | NULL  | 20     |
| 7654  | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250 | 1400  | 30     |
| 7698  | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850 | NULL  | 30     |
| 7782  | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450 | NULL  | 20     |
| 7788  | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3000 | NULL  | 40     |
| 7839  | KING   | PRESIDENT | NULL | 1981-11-17 | 5000 | NULL  | 20     |
| 7844  | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500 | 0     | 30     |
| 7876  | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1100 | NULL  | 20     |
| 7900  | JAMES  | CLERK     | 7698 | 1981-12-03 | 950  | NULL  | 30     |
| 7902  | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000 | NULL  | 20     |
+-------+--------+-----------+------+------------+------+-------+--------+
```
## 03. Increase salary by 10% for DEPTNO = 20

```sql
UPDATE EMPLOYEE_MASTER
SET SAL = SAL * 1.10
WHERE DEPTNO = 20;

---------------------------------------
TABLE
SELECT * FROM EMPLOYEE_MASTER;
```

```
+-------+--------+-----------+------+------------+------+-------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL  | COMM  | DEPTNO |
+-------+--------+-----------+------+------------+------+-------+--------+
| 7369  | SMITH  | CLERK     | 7902 | 1980-12-17 |  880 | NULL  | 20     |
| 7499  | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600 | 300   | 30     |
| 7521  | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250 | 300   | 30     |
| 7566  | JONES  | MANAGER   | 7839 | 1981-04-02 | 3273 | NULL  | 20     |
| 7654  | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250 | 1400  | 30     |
| 7698  | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850 | NULL  | 30     |
| 7782  | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2695 | NULL  | 20     |
| 7788  | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3000 | NULL  | 40     |
| 7839  | KING   | PRESIDENT | NULL | 1981-11-17 | 5500 | NULL  | 20     |
| 7844  | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500 | 0     | 30     |
| 7876  | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1210 | NULL  | 20     |
| 7900  | JAMES  | CLERK     | 7698 | 1981-12-03 |  950 | NULL  | 30     |
| 7902  | FORD   | ANALYST   | 7566 | 1981-12-03 | 3300 | NULL  | 20     |
+-------+--------+-----------+------+------------+------+-------+--------+
```

---

## 04. Modify SAL column to DECIMAL(10,2)

```sql
ALTER TABLE EMPLOYEE_MASTER
MODIFY SAL DECIMAL(10,2);

---------------------------------------
TABLE
SELECT * FROM EMPLOYEE_MASTER;
```

```
+-------+--------+-----------+------+------------+-----------+-------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL       | COMM  | DEPTNO |
+-------+--------+-----------+------+------------+-----------+-------+--------+
| 7369  | SMITH  | CLERK     | 7902 | 1980-12-17 |  880.00   | NULL  | 20     |
| 7566  | JONES  | MANAGER   | 7839 | 1981-04-02 | 3273.00   | NULL  | 20     |
| 7782  | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2695.00   | NULL  | 20     |
| 7839  | KING   | PRESIDENT | NULL | 1981-11-17 | 5500.00   | NULL  | 20     |
| 7876  | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1210.00   | NULL  | 20     |
| 7902  | FORD   | ANALYST   | 7566 | 1981-12-03 | 3300.00   | NULL  | 20     |
+-------+--------+-----------+------+------------+-----------+-------+--------+
```

---

## 05. Drop EMPLOYEE_MASTER Table

```sql
DROP TABLE EMPLOYEE_MASTER;
```

```
Query OK, 0 rows affected
```


