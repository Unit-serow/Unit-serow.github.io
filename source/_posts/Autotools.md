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
autotools是一个工具集，并它包含了以下程序
* aclocal
* autoscan
* autoconf
* autoheader
* automake

---

**aclocal**
aclocal(automake)
* 根据已安装的宏，用户定义宏和aclocal.m4文件中的宏将configure.ac文件所需要的宏集中定义到文件aclocal.m4文件中
* aclocal由perl脚本所编写，而aclocal的定义为 `aclocal - create aclocal.m4 by scanning configure.ac`
* aclocal是一个由perl编写的脚本程序
* aclocal根据configure.in文件中的宏所定义的内容，自动生成aclocal.m4文件


---

**autoscan**
autoscan(autoconf)
* 用于扫描源代码以搜寻普通的可移植性问题，如检查编译器，库，头文件等
* 从而生成文件configure.scan，它是configure.ac的原型之一
或
执行逻辑:
* autoscan工具用来扫描文件目录，可以用目录名作为参数，如果不使用参数的话，autoscan将会扫描当前所使用的目录
* 之后autoscan将从所指定的扫描目录中，将由扫描得到此目录下的源代码文件，基于此源代码生成源代码的configure.scan文件
* configure.scan文件用于当作configure.in文件的模板，以此来获取configure.in文件
* 而configure.in的内容是一些宏，这些宏将经由autoconf工具处理并生成configure脚本

---

**autoheader**
autoheader(autoconf)
根据configure.ac中的某些宏，运行m4,
如ccp宏定义则声称config.h.in

---

**Automake**
automake工具用于处理由事先编写好且带有预定义宏的文件，并生成makefile
简述:
* 首先使用automake工具根据configure.in和Makefile.am来生成Makefile.in
* 然后编写宏定义文件makefile.in，再然后根据autoconf生成的configure脚本文件，最后让configure依据makefile.in来生成一个与之源码对应的makefile文件
或
* automake将makefile.am中定义的结构建立起makefile.in，然后configure脚本将生成的makefile.in文件转换为makefie
* 如果在configure.ac中有特殊定义的宏，比如AC-PROG-LIBTOOL,automake会调用libtoolize，否则产生config.guess和config.sub

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
* autoconf工具用于根据configure.in文件和alocal.m4文件来产生configure文件
* 而此时的aclocal.m4需要用到GNU M4工具去处理
* config是一个脚本，它能够设置源代码程序来适应各种不同的操作系统平台
* 并且根据不同的操作系统来产生合适的Makefile
* 从而使所扫描到的源代码程序能在不同的操作系统平台上被编译出来
或
* 作用是将configure.ac中的宏展开，生成configure脚本-一个shell脚本，此过程中可能需要用到aclocal.m4中定义的宏
* 以达成自动配置软件源代码包

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

---

**逻辑简述:**
* 利用autotool组件生成configure脚本后生成makefile的执行逻辑
* 要生成makefile之前需要编写makefile.am文件之后再让automake工具使用autoconf所生成的configure脚本来生成所选源码文件的makefile
* 第一步需要先执行autoscanf命令来扫描当前目录下的源码文件，然后autoscanf会基于源码文件生成一个configure.scan文件
* 基于源码生成的configure.scan文件被用于当做configure.in文件的模板而存在
* 第二步将configure.scan的文件名改为configure.in，并对configure.in内的各种宏定义进行修改，这些宏定义内包括了用于让指向让autoconf处理configure.in文件从而生成从configure脚本
* 第三步执行aclocal命令，生成alocal.m4文件，因为autoconf需要aclocal.m4文件来生成configure脚本文件
* 第四步执行autoconf命令，生成configure脚本文件(自动配置源代码脚本文件)
* 第五步编写makefile.am文件，makefile.am文件用于描述定义从而让automake生成指定的宏和目标
* 第六步运行automake命令，可以增加参数--add-missing，从而让automake自动添加一些脚本文件
* 第七步运行configure脚本，从而生成基于源代码的makefile文件
* 最后直接使用make工具，编译并编译安装makefile就可以了，make install将会直接把可执行文件安装再/usr/local/目录下，至此完毕


以上五个程序皆可称为M4宏的扩展包,文件处理的步骤与顺序，逻辑关系，应用等深度刨析第一部分里不做赘述
以上内容仅为主观理解，仅供参考

---
