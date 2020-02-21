---
title: SQL-3
date: 2020-02-19 21:45:01
tags: [随笔]
categories: [软件,数据库]
---

### SQL-1/SQL2 补充内容

**增/删/改/查(SQL涉及概念补充):**

* 增/改
> 序列(AUTO INCREMENT)
> 插入(INSERT INTO)
> 更新(UPDATE)
> 创建(CREATE)
> 修改与创建(ALTER)

* 查
> 唯一值(DISTINCT)
> 条件(逻辑)语句(WHERE/LIKE/AND&OR/IN/BETWEEN)
> 排序(ORDER BY)
> 限制返回数量(TOP,LIMIT,ROWNUM)

* 删
> DELETE
> DROP

---

**通用概念总览:**

* 通配符
* 通用数据类型
* DB 数据类型
* 别名(AS)
* 视图(VIEW)
* 日期(DATES)
* 索引(INDEX)
* 合并(UNION)
* NULL(NULL值，NULL函数，NULL约束)
* 复制(SELECT INTO/INSERT INTO SELECT)
* 连接(JOIN/(INNER,LEFT,RIGHT,OUTER,FULL))
* 约束(Constraints(NOT NULL/UNIQUE/PRIMARY KEY/FOREIGN KEY/CHECK/DEFAULT))
* 函数(聚合函数/其它函数)

---

**JDBC**
* JDBC API允许用户访问任何形式的表格数据，尤其是存储在关系数据库中的数据
* 执行流程:
1. 连接数据源，如：数据库
2. 为数据库传递查询和更新指令
3. 处理数据库响应并返回的结果

---

**ODBC**
* 开放数据库互连(Open DataBase Connectivity)
* 是微软公司开放服务结构(WOSA，Windows Open Services Architecture)中有关数据库的一个组成部分
* 它建立了一组规范，并提供了一组对数据库访问的标准API(应用程序编程接口)
* 这些API利用SQL来完成其大部分任务
* ODBC本身也提供了对SQL语言的支持，用户可以直接将SQL语句送给ODBC

---

**PowerBuilder/PB**
* 是美国Sybase公司研制的一种新型，快速开发工具，结构为C/S(客户机/服务器结构)
* 是基于Windows3.x、Windows95和WindowsNT的一个集成化开发工具
* 它包含一个直观的图形界面和可扩展的面向对象的编程语言PowerScript，提供与当前流行的大型数据库的接口，并通过ODBC与单机数据库相连

---

**PL/SQL**
* ORACLE客户端连接器

**CYNOSDB**
* 云数据库(Cynosdb)

---

### Oracle-PL/SQL

* 客户端与连接工具

**解释:**

* Oracle Database Software Express Edition 精简版
* Oracle Database Software Enterprise Edition 企业版

---

**参考资料:**

**客户端(Client):**

* 安装指南[跳转](https://docs.oracle.com/en/database/oracle/oracle-database/18/xeinl/lot.html)
> `https://docs.oracle.com/en/database/oracle/oracle-database/18/xeinl/lot.html`

* 文档/手册[跳转](https://docs.oracle.com/en/database/oracle/oracle-database/18/index.html)
> https://docs.oracle.com/en/database/oracle/oracle-database/
> `https://docs.oracle.com/en/database/oracle/oracle-database/18/index.html`

* EN-文献资料[跳转](https://docs.oracle.com/en/)
> `https://docs.oracle.com/en/`

* 获取地址[跳转](https://www.oracle.com/database/technologies/oracle-database-software-downloads.html#19c)
> `https://www.oracle.com/database/technologies/oracle-database-software-downloads.html#19c`

* 官方网站[跳转](https://www.oracle.com/index.html)
> `https://www.oracle.com/index.html`

* CN-文档[跳转](https://www.oracle.com/technetwork/cn/indexes/documentation/index.html)
> `https://www.oracle.com/technetwork/cn/indexes/documentation/index.html`

---
