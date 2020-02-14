---
title: RDBMS MySQL-1
date: 2020-02-14 04:01:01
tags: RDBMS
categories: [软件,数据库]
---

### MySQL-1

**应用-1**

**所使用数据模型:**
> 六行六列
> TABLES1:
```
[ID-A-B-C-D-time]
[1-1-2-3-4-now]
[2-1-2-3-4-now]
[3-1-2-3-4-now]
[4-1-2-3-4-now]
[5-2-3-4-5-2020-02-13]
```
> TABLES2:
```
[ID-A-B-C-D-time]
[1-1-2-3-4-now]
[2-2-3-4-5-now]
[3-2-3-4-5-now]
[4-2-3-4-5-now]
[5-2-3-4-5-2020-02-13]
```
> TABLES3:
```
[ID-A-B-C-D-time]
[1-1-2-3-4-now]
[2-2-3-4-5-now]
[3-6-7-8-9-now]
[4-6-7-8-9-now]
[5-6-7-8-9-2020-02-13]
```

---

```
SHOW DATABASELS;
CREATE DATABASE TEST1;
USE TEST1;
```

```
MariaDB [(none)]> CREATE DATABASE TEST1;
Query OK, 1 row affected (0.000 sec)

MariaDB [(none)]> USE TEST1;
Database changed
```

**分别创建TABLES1,TABLES2,TABLES3**

```
CREATE TABLE TABLES1(
ID INT NOT NULL AUTO_INCREMENT,
A VARCHAR(100) NOT NULL,
B VARCHAR(100) NOT NULL,
C VARCHAR(100) NOT NULL,
D VARCHAR(100) NOT NULL,
TIME DATE,
PRIMARY KEY ( ID )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

```
CREATE TABLE TABLES2(
ID INT NOT NULL AUTO_INCREMENT,
A VARCHAR(100) NOT NULL,
B VARCHAR(100) NOT NULL,
C VARCHAR(100) NOT NULL,
D VARCHAR(100) NOT NULL,
TIME DATE,
PRIMARY KEY ( ID )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

```
CREATE TABLE TABLES3(
ID INT NOT NULL AUTO_INCREMENT,
A VARCHAR(100) NOT NULL,
B VARCHAR(100) NOT NULL,
C VARCHAR(100) NOT NULL,
D VARCHAR(100) NOT NULL,
TIME DATE,
PRIMARY KEY ( ID )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

```
MariaDB [TEST1]> CREATE TABLE TABLES1(
    -> ID INT NOT NULL AUTO_INCREMENT,
    -> A VARCHAR(100) NOT NULL,
    -> B VARCHAR(100) NOT NULL,
    -> C VARCHAR(100) NOT NULL,
    -> D VARCHAR(100) NOT NULL,
    -> TIME DATE,
    -> PRIMARY KEY ( ID )
    -> )ENGINE=InnoDB DEFAULT CHARSET=utf8;
Query OK, 0 rows affected (0.046 sec)
```

```
MariaDB [TEST1]> CREATE TABLE TABLES2(
    -> ID INT NOT NULL AUTO_INCREMENT,
    -> A VARCHAR(100) NOT NULL,
    -> B VARCHAR(100) NOT NULL,
    -> C VARCHAR(100) NOT NULL,
    -> D VARCHAR(100) NOT NULL,
    -> TIME DATE,
    -> PRIMARY KEY ( ID )
    -> )ENGINE=InnoDB DEFAULT CHARSET=utf8;
Query OK, 0 rows affected (0.043 sec)
```

```
MariaDB [TEST1]> CREATE TABLE TABLES3(
    -> ID INT NOT NULL AUTO_INCREMENT,
    -> A VARCHAR(100) NOT NULL,
    -> B VARCHAR(100) NOT NULL,
    -> C VARCHAR(100) NOT NULL,
    -> D VARCHAR(100) NOT NULL,
    -> TIME DATE,
    -> PRIMARY KEY ( ID )
    -> )ENGINE=InnoDB DEFAULT CHARSET=utf8;
Query OK, 0 rows affected (0.005 sec)
```

`SHOW TABLES;`

```
MariaDB [TEST1]> SHOW TABLES;
+-----------------+
| Tables_in_TEST1 |
+-----------------+
| TABLES1         |
| TABLES2         |
| TABLES3         |
+-----------------+
3 rows in set (0.001 sec)
```

---

**分别向TABLES1,TABLES2,TABLES3内填充数据**
```
BEGIN;
SET AUTOCOMMIT=0;
SAVEPOINT A;
```

* 4
```
INSERT INTO TABLES1
(A,B,C,D,TIME)
VALUES
("1","2","3","4",NOW());
```
* 1
```
INSERT INTO TABLES1
(A,B,C,D,TIME)
VALUES
("2","3","4","5",'2020-02-13');
```

```
MariaDB [TEST1]> INSERT INTO TABLES1
    -> (A,B,C,D,TIME)
    -> VALUES
    -> ("1","2","3","4",NOW());
Query OK, 1 row affected, 1 warning (0.000 sec)
```

```
MariaDB [TEST1]> INSERT INTO TABLES1 (A,B,C,D,TIME) VALUES ("1","2","3","4",NOW());
Query OK, 1 row affected, 1 warning (0.000 sec)

MariaDB [TEST1]> INSERT INTO TABLES1 (A,B,C,D,TIME) VALUES ("1","2","3","4",NOW());
Query OK, 1 row affected, 1 warning (0.000 sec)

MariaDB [TEST1]> INSERT INTO TABLES1 (A,B,C,D,TIME) VALUES ("1","2","3","4",NOW());
Query OK, 1 row affected, 1 warning (0.000 sec)
```

```
MariaDB [TEST1]> INSERT INTO TABLES1
    -> (A,B,C,D,TIME)
    -> VALUES
    -> ("2","3","4","5",'2020-02-13');
Query OK, 1 row affected (0.000 sec)
```

```
RELEASE SAVEPOINT A;
SELECT * FROM TABLES1;
```

```
MariaDB [TEST1]> RELEASE SAVEPOINT A;
Query OK, 0 rows affected (0.000 sec)

MariaDB [TEST1]> SELECT * FROM TABLES1;
+----+---+---+---+---+------------+
| ID | A | B | C | D | TIME       |
+----+---+---+---+---+------------+
|  1 | 1 | 2 | 3 | 4 | 2020-02-14 |
|  2 | 1 | 2 | 3 | 4 | 2020-02-14 |
|  3 | 1 | 2 | 3 | 4 | 2020-02-14 |
|  4 | 1 | 2 | 3 | 4 | 2020-02-14 |
|  5 | 2 | 3 | 4 | 5 | 2020-02-13 |
+----+---+---+---+---+------------+
5 rows in set (0.000 sec)
```

```
RELEASE SAVEPOINT A;
COMMIT WORK;
```

---

```
STRAT TRANSACTION/BEGIN;
SET AUTOCOMMIT=0;
SAVEPOINT A;
```

```
* 1
INSERT INTO TABLES2
(A,B,C,D,TIME)
VALUES
("1","2","3","4",NOW());
```
* 3
```
INSERT INTO TABLES2
(A,B,C,D,TIME)
VALUES
("2","3","4","5",NOW());
```
* 1
```
INSERT INTO TABLES2
(A,B,C,D,TIME)
VALUES
("2","3","4","5",'2020-02-13');
```

```
MariaDB [TEST1]> INSERT INTO TABLES2
    -> (A,B,C,D,TIME)
    -> VALUES
    -> ("1","2","3","4",NOW());
Query OK, 1 row affected, 1 warning (0.002 sec)
```

```
MariaDB [TEST1]> INSERT INTO TABLES2
    -> (A,B,C,D,TIME)
    -> VALUES
    -> ("2","3","4","5",NOW());
Query OK, 1 row affected, 1 warning (0.001 sec)
```

```
MariaDB [TEST1]> INSERT INTO TABLES2 (A,B,C,D,TIME) VALUES ("2","3","4","5",NOW());
Query OK, 1 row affected, 1 warning (0.001 sec)

MariaDB [TEST1]> INSERT INTO TABLES2 (A,B,C,D,TIME) VALUES ("2","3","4","5",NOW());
Query OK, 1 row affected, 1 warning (0.001 sec)
```

```
MariaDB [TEST1]> INSERT INTO TABLES2
    -> (A,B,C,D,TIME)
    -> VALUES
    -> ("2","3","4","5",'2020-02-13');
Query OK, 1 row affected (0.001 sec)
```

`SELECT * FROM TABLES2;`

```
MariaDB [TEST1]> SELECT * FROM TABLES2;
+----+---+---+---+---+------------+
| ID | A | B | C | D | TIME       |
+----+---+---+---+---+------------+
|  1 | 1 | 2 | 3 | 4 | 2020-02-14 |
|  2 | 2 | 3 | 4 | 5 | 2020-02-14 |
|  3 | 2 | 3 | 4 | 5 | 2020-02-14 |
|  4 | 2 | 3 | 4 | 5 | 2020-02-14 |
|  5 | 2 | 3 | 4 | 5 | 2020-02-13 |
+----+---+---+---+---+------------+
5 rows in set (0.000 sec)
```

```
RELEASE SAVEPOINT A;
COMMIT WORK;
```

---

```
STRAT TRANSACTION/BEGIN; 
SET AUTOCOMMIT=0;
SAVEPOINT A;
```

* 1
```
INSERT INTO TABLES3
(A,B,C,D,TIME)
VALUES
("1","2","3","4",NOW());
```
* 1
```
INSERT INTO TABLES3
(A,B,C,D,TIME)
VALUES
("2","3","4","5",NOW());
```
* 2
```
INSERT INTO TABLES3
(A,B,C,D,TIME)
VALUES
("6","7","8","9",NOW());
```
* 1
```
INSERT INTO TABLES3
(A,B,C,D,TIME)
VALUES
("6","7","8","9",'2020-02-13');
```

```
MariaDB [TEST1]> INSERT INTO TABLES3
    -> (A,B,C,D,TIME)
    -> VALUES
    -> ("1","2","3","4",NOW());
Query OK, 1 row affected, 1 warning (0.001 sec)
```

```
MariaDB [TEST1]> INSERT INTO TABLES3
    -> (A,B,C,D,TIME)
    -> VALUES
    -> ("2","3","4","5",NOW());
Query OK, 1 row affected, 1 warning (0.001 sec)
```

```
MariaDB [TEST1]> INSERT INTO TABLES3
    -> (A,B,C,D,TIME)
    -> VALUES
    -> ("6","7","8","9",NOW());
Query OK, 1 row affected, 1 warning (0.001 sec)
```

```
MariaDB [TEST1]> INSERT INTO TABLES3 (A,B,C,D,TIME) VALUES ("6","7","8","9",NOW());
Query OK, 1 row affected, 1 warning (0.001 sec)
```

```
MariaDB [TEST1]> INSERT INTO TABLES3
    -> (A,B,C,D,TIME)
    -> VALUES
    -> ("6","7","8","9",'2020-02-13');
Query OK, 1 row affected (0.001 sec)
```

`SELECT * FROM TABLES3;`

```
MariaDB [TEST1]> SELECT * FROM TABLES3;
+----+---+---+---+---+------------+
| ID | A | B | C | D | TIME       |
+----+---+---+---+---+------------+
|  1 | 1 | 2 | 3 | 4 | 2020-02-14 |
|  2 | 2 | 3 | 4 | 5 | 2020-02-14 |
|  3 | 6 | 7 | 8 | 9 | 2020-02-14 |
|  4 | 6 | 7 | 8 | 9 | 2020-02-14 |
|  5 | 6 | 7 | 8 | 9 | 2020-02-13 |
+----+---+---+---+---+------------+
5 rows in set (0.000 sec)
```

```
RELEASE SAVEPOINT A;
COMMIT WORK;
```

---

**从三个表中选择所有列A匹配1的数据，返回所有列A中映射于列1的数据，并让列A靠左**

```
SELECT A,B FROM TABLES1
WHERE A='1'
UNION ALL
SELECT A,B FROM TABLES2
WHERE A='1'
UNION ALL
SELECT A,B FROM TABLES3
WHERE A='1'
ORDER BY A;
```

```
MariaDB [TEST1]> SELECT A,B FROM TABLES1
    -> WHERE A='1'
    -> UNION ALL
    -> SELECT A,B FROM TABLES2
    -> WHERE A='1'
    -> UNION ALL
    -> SELECT A,B FROM TABLES3
    -> WHERE A='1'
    -> ORDER BY A;
+---+---+
| A | B |
+---+---+
| 1 | 2 |
| 1 | 2 |
+---+---+
2 rows in set (0.001 sec)
```

**查询并输出表TABLES1内列A中匹配数值2和列B中匹配数值3与列TIME中匹配以3结尾的数据**
> `SELECT * FROM TABLES1 WHERE A=2 AND B=3 AND TIME LIKE '%3';`
```
MariaDB [TEST1]> SELECT * FROM TABLES2 WHERE A=2 AND B=3 AND TIME LIKE '%3';
+----+---+---+---+---+------------+
| ID | A | B | C | D | TIME       |
+----+---+---+---+---+------------+
|  5 | 2 | 3 | 4 | 5 | 2020-02-13 |
+----+---+---+---+---+------------+
1 row in set (0.000 sec)
```

---

**将表A内数据利用COUNT()函数按数值类型进行数据分组并求其平均值,并按降序排列(默认升序)**

> `SELECT A, COUNT(*) FROM TABLES2 GROUP BY A DESC;`

```
MariaDB [TEST1]> SELECT A, COUNT(*) FROM TABLES2 GROUP BY A DESC;
+---+----------+
| A | COUNT(*) |
+---+----------+
| 2 |        4 |
| 1 |        1 |
+---+----------+
2 rows in set (0.000 sec)
```

---

**TABLES1&TABLES2-left&right**
**将TABLES1的A,B列与TABLES2的B,C列进行以下三种连接:**
**将标识为a的A,B列于标识为b的C列进行等值连接**

```
SELECT a.A, a.B, b.C FROM TABLES1 a INNER JOIN TABLES2 b ON a.B = b.B; 
SELECT a.A, a.B, b.C FROM TABLES1 a, TABLES2 b WHERE a.B = b.B;
```

* 左连接:
> `SELECT a.A, a.B, b.C FROM TABLES1 a LEFT JOIN TABLES2 b ON a.B = b.B;`
* 右连接:
> `SELECT a.A, a.B, b.C FROM TABLES1 a RIGHT JOIN TABLES2 b ON a.B = b.B;`

**如下所示:**

```
MariaDB [TEST1]> SELECT a.A, a.B, b.C FROM TABLES1 a INNER JOIN TABLES2 b ON a.B = b.B; 
+---+---+---+
| A | B | C |
+---+---+---+
| 1 | 2 | 3 |
| 1 | 2 | 3 |
| 1 | 2 | 3 |
| 1 | 2 | 3 |
| 2 | 3 | 4 |
| 2 | 3 | 4 |
| 2 | 3 | 4 |
| 2 | 3 | 4 |
+---+---+---+
8 rows in set (0.000 sec)
```

```
MariaDB [TEST1]> SELECT a.A, a.B, b.C FROM TABLES1 a LEFT JOIN TABLES2 b ON a.B = b.B; 
+---+---+------+
| A | B | C    |
+---+---+------+
| 1 | 2 | 3    |
| 1 | 2 | 3    |
| 1 | 2 | 3    |
| 1 | 2 | 3    |
| 2 | 3 | 4    |
| 2 | 3 | 4    |
| 2 | 3 | 4    |
| 2 | 3 | 4    |
+---+---+------+
8 rows in set (0.000 sec)
```

```
MariaDB [TEST1]> SELECT a.A, a.B, b.C FROM TABLES1 a RIGHT JOIN TABLES2 b ON a.B = b.B;
+------+------+---+
| A    | B    | C |
+------+------+---+
| 1    | 2    | 3 |
| 1    | 2    | 3 |
| 1    | 2    | 3 |
| 1    | 2    | 3 |
| 2    | 3    | 4 |
| 2    | 3    | 4 |
| 2    | 3    | 4 |
| 2    | 3    | 4 |
+------+------+---+
8 rows in set (0.000 sec)
```

---
