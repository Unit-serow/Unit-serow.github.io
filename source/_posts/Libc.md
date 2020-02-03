---
title: GNU C libary/Libc
date: 2020-02-02 00:47:10
tags: [GNU/Linux,1.认识与概述]
categories: [软件,GNU]
---

### GNU C Library 第一章节

**C 标准函数库 Libc**

**概述:**
* GNU/Linux操作系统一个重要的组成部分
* FSF为GNU所写，作用是配合linux内核,是Linux下基于ANSI C[^1]标准的GNU C[^2]标准函数库
[^1]: 由美国国家标准局所制定的C语言发布标准-是最基本的C语言函数库，包含了C语言最基本的库函数并且是C语言最初的标准
[^2]: 由LGPL许可协议发布的，自由的，公开源代码并且方便下载的C编译程序

**存在目的:**
* 目的是为linux内核的操作系统提供核心库文件，库提供了关键的API，当然也包括Linux内核的API
* 虽说称为C的标准函数库，但还支持很多其他的程序语言
---

**其它C 标准库**

C POSIX library
* C 可移植标准接口库
* 包含了一些在C 标准库之外的函数，这里指ANSI所定制的C 标准库

CRT/C Run-time Library
* C 运行时期库
* C 程序运行时需要这些库中的函数
* 包含于程序运行时使用到的一些API集合，这里的API是预先编译后存放在linux系统中的二进制代码形式的文件
* CRT通常作为C编译程序发布
* CRT含有初始化代码，还有错误处理代码(例如divide by zero处理)
---

**其它资料:**
ANSI C库可以根据头文件划分为15个类别
其中包括:
* 字符类型 ()
* 错误码()
* 浮点常数 ()
* 数学常数 ()
* 标准定义 ()
* 标准 I/O ()
* 工具函数 ()
* 字符串操作 ()
* 时间和日期 ()
* 可变参数表 ()
* 信号 ()
* 非局部跳转 ()
* 本地信息 ()
* 程序断言 () 等等
* 这在其他的C语言的IDE中都是有的

以上内容引用自百度百科[条目](https://baike.baidu.com/item/libc)
---

参考资料:

GNU C Library连接[跳转](https://www.gnu.org/software/libc/involved.html)
`https://www.gnu.org/software/libc/involved.html`

C POSIX库参考文献[跳转](https://web.archive.org/web/20100724201155/http://www.space.unibe.ch/comp_doc/c_manual/C/FUNCTIONS/funcref.htm)
`https://web.archive.org/web/20100724201155/http://www.space.unibe.ch/comp_doc/c_manual/C/FUNCTIONS/funcref.htm`

C 标准函式库[跳转](https://pubs.opengroup.org/onlinepubs/9699919799/idx/head.html)
`https://pubs.opengroup.org/onlinepubs/9699919799/idx/head.html`

C POSIX library-wiki[跳转](https://zh.wikipedia.org/wiki/C_POSIX_library)
`https://zh.wikipedia.org/wiki/C_POSIX_library`










