---
title: GNU Binutils
date: 2020-02-01 21:52:49
tags: [GNU/Linux,1.认识与概述]
categories: [软件,GNU]
---

### GNU Binutils 第一部分

**GNU 二进制工具包**

**工具包内包含程序**
主要包含ld与as，分别是GNU链接器-GAS与GNU汇编器-GLD

**其他程序**
* ar-用于建立，修改，提取归档文件(archive)[^1]/用于对归档/静态库做创建，修改和提取的操作
* addr2line-将目标文件的虚拟地址转换为文件的行号或符号
* c++filt-解码C++的符号
* dlltool-用于构建与使用DLL文件，也就是创建windows动态库
* gold-正在测试的功能，一个新型且效率更高的ELF的链接器
* ELF是一种用于可执行文件，目标文件，共享库和核心转储的标准文件格式，可执行与可连接格式，ELF所产生的数据结构与工具不做阐述
* gprof-用于显示性能的分析信息/性能分析工具
* nlmconv-将目标代码转换为NetWare Loadable Module/NLM文件格式
* nm-列出并显示目标文件中的符号
* objcopy-复制并编译目标文件，其过程中可以修改
* objdump-显示目标文件中的相关信息，可用于反汇编
* ranlib-生成静态库索引
* readelf-用于显示任何ELF格式文件的内容
* size-列出对象总体或归档文件的节数/大小
* strings-列出目标二进制文件中的可打印/可显示字符串
* strip-从目标文件中移除符号
* windmc-兼容windows消息的编译器，用于产生windows的消息资源
* windres-windows资源文件的编译器
---

**杂项及存在意义**
* 大部分的复杂代码都存于Binary File Descriptor library和libopcodes库内
* 所以它是一整套编程语言工具程序,用于处理许多格式的目标文件
* 这些程序大多数使用BFD-二进制文件描述库
* 主要的目的还是为GNU项目用于解决不同格式的目标文件的可移植性问题的主要机制
---

**参考:**

获取：
```
http://ftp.gnu.org/gnu/binutils
http://ftpmirror.gnu.org/binutils
apt-get install binutils*
克隆：git clone git://sourceware.org/git/binutils-gdb.git
```

官网[跳转](https://www.gnu.org/software/binutils/binutils.html)
`https://www.gnu.org/software/binutils/binutils.html`

文档[跳转](https://sourceware.org/binutils/docs-2.33.1/)
`https://sourceware.org/binutils/docs-2.33.1/`

[^1]: archive是一个包含多个被包含文件的单一库文件,它可以保证从中检索到原始的被包含文件-mumber,而member用于保存archive的各种基本属性，当member被提取后，archive的属性将被还原到初始状态

