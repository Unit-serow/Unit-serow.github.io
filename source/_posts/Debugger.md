---
title: GNU Debugger
date: 2020-02-01 18:36:47
tags: [GNU/Linux,1.认识与概述]
categories: [软件,GNU]
---

### GNU Debugger 第一部分

**GNU 调试工具 GDB**

**概述:**

存在的意义/作用:

* GDB大多数UNIX及UNIX-like下的调试工具
* GDB可以根据自定义的要求启动所选程序
* 让被调试的程序在指定的调试断点停住，其断点可以是条件表达式，当程序被停住时可以去检查该程序中正在处理的事务
* GDB还可以用于修改程序，以此来修复BUG所带来的影响
* GDB相比于其他具有GUI的调式工具的优点就是具有修复网络断点以及恢复链接等功能
* 还可以把GDB理解为一个强大的命令行调试工具，命令行的优点就是可以形成一个完整的执行序列，以此来形成脚本程序[^1]
[^1]: 因为UNIX下的软件基本上都是命令行的，所以它们具有天生的优势-可以很方便的把简单的已有工具的命令集成在一起，从而做出一个功能强大的程序
---

**使用方法简述:**

**启动**
* 可以直接执行GDB以启动GDB命令行，`quit`退出GDB命令行
* 执行`gdb file name`来选中被调试的目标文件，并进入GDB命令行
* `run`用于执行程序，后面可以接GDB已有的缺省参数

**断点**
* 执行break命令，可以简写为b，用来给调试的程序中设置断点
* 从断电处继续运行执行continue命令
* GDB还内置了断点的管理工具
* `info break` 用于显示当前GDB所有的断点信息
* `break breakpoint 编号` 用于删除指定编号的断点，如果不带编号将删除所有的断点
* `disable breakpoint 编号` 用于禁止使用指定编号的断点，同时info break的enb域变为n
* `enable breakpoint 编号` 允许指定断点，同时info break的enb域变为y

**其他功能简述**
* 单步执行：next不进入单步执行，step进入单步执行
* 函数调用：call function name调用和执行一个函数，执行finish结束当前的函数，如果有返回值就会显示其返回值
* 机器语言工具，信号处理与变量复制的检查
---

**参考资料:**

官方网站[跳转](https://www.gnu.org/software/gdb/)
https://www.gnu.org/software/gdb/

GDB手册[跳转](https://sourceware.org/gdb/current/onlinedocs/gdb/)
https://sourceware.org/gdb/current/onlinedocs/gdb/

深入GDB[跳转](https://web.archive.org/web/20080616054054/http://sources.redhat.com/gdb/current/onlinedocs/gdbint.html)
https://web.archive.org/web/20080616054054/http://sources.redhat.com/gdb/current/onlinedocs/gdbint.html

开源程序的体系结构-GDB[跳转](http://www.aosabook.org/en/gdb.html)
http://www.aosabook.org/en/gdb.html
http://www.aosabook.or

---
