---
title: GNU Libtool
date: 2020-02-01 22:58:21
tags: [GNU/Linux,1.认识与概述]
categories: [软件,GNU]
---

### GNU libtool 第一章节

**GNU 构建系统**

**概述与解释:**
* GNU Libtool是一种属于[GNU构建系统](https://unit-serow.github.io/2020/01/29/Autotools/)的GNU程序设计工具
* GNU Libtool是一个用于支持通用库的脚本程序
* 用于解决在不同的操作系统中使用共享库进行代码移植的复杂性，在不同的系统中建立动态链接库，以隐藏不同系统之间的差异性
* 从而给开发人员提供一致的接口
* 但还是需要底层系统对所创建链接库的支持，所以libtool不能在不支持动态连接库的系统中创建动态链接库
---

**存在目的:**
* 用于产生/建立便携式的库，它既可以建立动态链接库，也可以建立动态链接库，还可以包含两者
* GNU libtool的目的是使每一个主机类型的完整功能都可以通过一个泛用接口来产生
* GNU libtool的目标是使接口一致
---

**使用方法**
本章节不对应用进行过多阐述
libtool通常与GNU建构系统中的autoconf和automake这两个工具一起使用
需要参照系统手册（构建通用库所需要执行的命令）以及修改相应makefile的makefile.in或makefile.in文件
相关内容可查询[libtool文档](https://www.gnu.org/software/libtool/manual/libtool.html)
---

参考资料

GNU Libtool手册[跳转](https://www.gnu.org/software/libtool/manual/libtool.html)
`https://www.gnu.org/software/libtool/manual/libtool.html`

使用GNU Libtoo创建库[跳转](https://www.ibm.com/developerworks/cn/aix/library/1007_wuxh_libtool/index.html)
`https://www.ibm.com/developerworks/cn/aix/library/1007_wuxh_libtool/index.html`

官方网站[跳转](https://www.gnu.org/software/libtool/news.html)
`https://www.gnu.org/software/libtool/news.html`

autobook[跳转](http://www.sourceware.org/autobook/)
`http://www.sourceware.org/autobook/`

获取:
```
http: http://ftpmirror.gnu.org/libtool/
ftp: ftp://ftp.gnu.org/gnu/libtool/ 
克隆: git clone git://git.savannah.gnu.org/libtool.git
```





