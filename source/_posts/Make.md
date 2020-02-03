---
title: GNU Make
date: 2020-02-01 21:40:08
tags: [GNU/Linux,1.认识与概述]
categories: [软件,GNU]
---

### GNU Make 第一部分

**GNU 自动化建构**

**概述:**

* 在软件开发的过程中，make通常作为一个工具程序(unility software),经由makefile，从而实现自动化构建软件
* 在经由makefile时make工具会根据情况转换文件形式至target，转换的同时还会检查文件的依赖关系，检查依赖关系的方式本部分不做阐述
* 所以在编写软件时，应该先编写一个makefile，之后再让make去进行构建和安装

或称为

* 用于编译源代码，从而生成结果代码，然后将结果代码链接起来，最后生成可执行文件
* 其中名为makefile的文件用来确定某一target文件的以来关系，然后把生成target相关的命令转给机器的shell去执行

* IDE通常包含了make，make多用于UNIX下的软件开发
* 本质如同UNIX底层的其他基本程序，批量执行生成目标的命令，同时检查文件的依赖关系

---

参考
官方网站[跳转](https://www.gnu.org/software/make/make.html)
`https://www.gnu.org/software/make/make.html`

获取
`http: http://ftp.gnu.org/gnu/make/`
`ftp: ftp://ftp.gnu.org/gnu/make/`

make手册[跳转](https://www.gnu.org/software/make/manual/)
`https://www.gnu.org/software/make/manual/`

makefile手册[跳转](https://www.gnu.org/prep/standards/html_node/Makefile-Conventions.html#Makefile-Conventions)
`https://www.gnu.org/prep/standards/html_node/Makefile-Conventions.html#Makefile-Conventions`

make源码所在目录
```
/usr/share/doc/make/
/usr/local/doc/make/
```

make帮助指令
```
make --help
info make
man make
```

