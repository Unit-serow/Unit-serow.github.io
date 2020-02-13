---
title: SQL-1
date: 2020-02-12 16:15:56
tags: 随笔
categories: [软件,数据库]
---

### 结构化查询语言-SQL-1

**概述:**
* 全称`Structured Query Language`
* 是一种特定目的编程语言，用于管理关系型数据库管理系统(RDBMSR)，或在其中进行流处理
* RDBMS全称`Relational Database Management System`
* SQL是高级的非过程化编程语言
* 允许用户在高层数据结构上工作
* SQL同时也是数据库文件格式的扩展名
* SQL基于关系代数和元组关系演算，包括一个数据定义语言和数据操纵语言
* SQL在很大程度上是一种声明式编程(4GL)，但是其也含有过程式编程的元素
* 1986年的`SQL-86`/`SQL-87`是ANSI对于SQL的首次标准化
* 2016年的`SQL:2016`是现阶段最后一次标准化的更新
* SQL的核心大致可分为DQL,DDL,DML,DCL四大部分
* 本篇只进行基本的体系整理与概念认识与理解

---

**SQL语言内存在要素简述:**
> `子句`:基本构成条件，语句和查询的组成部分
> `语句`:由子句等任何其他元素构成的执行逻辑
> `查询`:基于特定条件检索数据
> `谓词`:限制语句和查询结果与控制流程
> `表达式`:用于产生任何标量值，标量值也可由列和行的数据库表构成
> `;`-`分号`:语句结束标志(终结符)，为SQL标准所定义
> 空格在SQL语句和查询中会被忽略

---

**SQL总体的构成包含五个部分:**
* 数据查询语言(Data Query Language，DQL)
* 数据定义语言(Data Definition Language，DDL)
* 数据操控语言(Data Manipulation Language, DML)
* 数据控制语言(Data Control Language, DCL)
* 事务控制语言

---

**SQL语言构成模块简述:**

1. DDL-数据定义语言
* SQL语言集中负责数据结构定义与数据库对象定义的语言
* 主要由`CREATE`,`ALTER`,`DROP`(`create`,`alter`,`drop`)三个语法构成
* SQL指令子的集之一

2. DML-数据操纵语言
* SQL中用于数据库操作，对数据库其中的对象和数据运行访问工作的编程语句
* 以`INSERT`,`UPDATE`,`DELETE`(`insert`,`update`,`delete`)作为核心
* 分别代表创建，修改，删除
* 再加上SQL的`SELECT`(`select`查询)语句(属于DQL)
* 从而称其为`CRUD`即为`增删改查`
* SQL指令集的子集之一

3. DCL-数据控制语言
* SQL中可对数据访问权进行控制的指令
* 由GRANT和REVOKE两个指令组成
* SQL指令集的子集之一

4. DQL-数据查询语言
* DQL的主要功能是查询数据
* SQL中用于从数据库或信息系统中查询数据的计算机语言
* 由`SELECT`,`FROM`,`WHERE`,`GROUP BY`和`ORDER BY`这些语法构成
* 其核心指令为`SELECT`(`select`)

---

**其他概念:**
* 语句，子句，关键字，运算符，操作符
* 通配符，连接，别名，约束，NULL，数据类型(通用/DB)

---

**参考:**
* SQL标准[参考资料/CN](https://web.archive.org/web/20100304063252/http://structedtext.appspot.com/db/sql.html)
> `https://web.archive.org/web/20100304063252/http://structedtext.appspot.com/db/sql.html`

