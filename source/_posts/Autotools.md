---
title: GNU  Autotools
subtitle: GNU 构建系统
date: 2020-01-29 19:08:58
tags: [GNU/Linux,1.认识与概述]
categories: [软件,GNU]
---

### GNU Autotools 第一部分

**GNU 构建系统**

**概述:**
autotools存在的目的就是用于生成makefile，从而实现降低makefile的维护难度与开发难度
autotools是一个工具集，它包含了一下程序
aclocal
autoscan
autoconf
autoheader
automake

---

**aclocal**
aclocal(automake)
根据已安装的宏，用户定义宏和acinclude.m4文件中的宏将configure.ac文件所需要的宏集中定义到文件aclocal.m4文件中
aclocal由perl脚本所编写，定义为 `aclocal - create aclocal.m4 by scanning configure.ac`

---

**autoscan**
autoscan(autoconf)
用于扫描源代码以搜寻普通的可移植性问题，如检查编译器，库，头文件等
从而生成文件configure.scan，它是configure.ac的原型之一

---

**autoheader**
autoheader(autoconf)
根据configure.ac中的某些宏，运行m4,
如ccp宏定义则声称config.h.in

---

**Automake**
automake将makefile.am中定义的结构建立起makefile.in，然后configure脚本将生成的makefile.in文件转换为makefie
如果在configure.ac中有特殊定义的宏，比如AC-PROG-LIBTOOL,automake会调用libtoolize，否则产生config.guess和config.sub

官方网站:https://www.gnu.org/software/automake/
[跳转](https://www.gnu.org/software/automake/)

官方文档:`https://www.gnu.org/software/automake/manual/automake.html`
[跳转](https://www.gnu.org/software/automake/manual/automake.html)

获取方式:
```
ftp: ftp://ftp.gnu.org/gnu/automake/ 
http: http://ftp.gnu.org/gnu/automake/ 
```
帮助指令: `automake --help`与`man automake`

---

**Autoconf**
作用是将configure.ac中的宏展开，生成configure脚本/shell脚本，此过程中可能需要用到aclocal.m4中定义的宏
以达成自动配置软件源代码包

官方网站: `https://www.gnu.org/software/autoconf/autoconf.html`
[跳转](https://www.gnu.org/software/autoconf/autoconf.html)

官方文档：`https://www.gnu.org/savannah-checkouts/gnu/autoconf/manual/autoconf-2.69/autconf.html`
[跳转](https://www.gnu.org/savannah-checkouts/gnu/autoconf/manual/autoconf-2.69/autoconf.html)

获取方式: 
```
ftp: ftp://ftp.gnu.org/gnu/autoconf/
http: http://ftp.gnu.org/gnu/autoconf/
git: git clone http://git.sv.gnu.org/r/autoconf.git
apt-get: apt-get install autoconf*
```
帮助指令: `autoconf --help`与`man autoconf`

---

**Autotools**

获取方式:
`apt-get install autotools`

以上五个程序皆可称为M4宏的扩展包,文件处理的步骤与顺序，逻辑关系，应用等深度刨析第一部分里不做赘述
以上内容仅为主观理解，仅供参考

---
