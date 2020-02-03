---
title: GNU Lib
date: 2020-01-30 10:43:52
tags: [1.认识与概述,GNU/Linux]
categories: [软件,GNU]
---

### GNU Lib 第一部分

**GNU 可移植性库**

**概述:**

* GNU Lib 存在的意义是实现所有gnu代码关于移植性问题处理方法的统一化
* 使任何基于GNU标准的软件，可以顺利的移植到任何其他的操作系统上，关于操作系统移植问题的方法统一化
* 所以可以把GNU Lib理解为所有基于GNU标准的软件的子程序，这些子程序将GNU软件互相链接，从而实现GNU软件包之间的完全共享
* 其中gcc因为libiberty库的原因，很难脱离GNU的构建树，但GNU Lib与其完全不同，构成它的子程序会实现资源等级的划分，使所有基于GNU协议的软件实现代码共享，从而解决移植性问题，而绝非去构建，安装或者链接库
* 因此GNU Lib没有发行版的概念，只需要将GNU Lib的源码复制到使用者的代码树中即可

---

### 其他

官网[跳转](https://www.gnu.org/software/gnulib)
`https://www.gnu.org/software/gnulib`

手册[跳转](https://www.gnu.org/software/gnulib/manual)
`https://www.gnu.org/software/gnulib/manual`

获取
`git clone git: //git.savannah.gnu.org/gnulib.git`

GNU Lib模块列表[跳转](https://www.gnu.org/software/gnulib/MODULES.html)
`https://www.gnu.org/software/gnulib/MODULES.html`

社区[跳转](http://git.savannah.gnu.org/gitweb/?=gnulib.get)
`http://savannah.gnu.org`
`http://git.savannah.gnu.org/gitweb/?p=gnulib.get`

帮助指令:`./gnulib-tool --help`

---
