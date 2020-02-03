---
title: GNU Binary File Descriptor/BFD
date: 2020-02-02 21:33:28
tags: [1.认识与概述,GNU/Linux]
categories: [软件,GNU]
---

### GNU Binary File Descriptor

**GNU 二进制文件描述 BFD**

**概述:**

* 目的是用于解决GNU项目中不同的目标文件的可移植性的主要机制
* 在GNU项目中对于不同目标文件可移植EFL[^1]性问题的主要解决机制
* BFD库还可以用来读取核心转储的结构化数据
* 截至至2003年，它支持25中不同体系结构的CPU上的大约50中文件格式
[^1]: ELF-可执行与可链接格式，Executable and Linkable Format简称为ELF
---

**BFD的设计逻辑与执行逻辑:**

* BFD通过对目标文件[^2]提供抽象视图来达成工作
* BFD在内部将数据从抽象视图转到目标处理器所规定的文件格式所要求的节与数据结构/字节布局等细节
* 它关键的作用是处理字节序的差异[^3],包括寻址[^4]算术等细节
* BFD最初的设计目的是可以成为被各种工具所使用的通用库，但为了达成这一目的就需要频繁修补API来解决系统所带来的影响与容纳新系统的功能，从而限制了它的使用模式与功能
* DFD的主要用户是[GAS](https://unit-serow.github.io/2020/02/01/Binutils/)，[GDL](https://unit-serow.github.io/2020/02/01/Binutils/)，[GNU Binutils](https://unit-serow.github.io/2020/02/01/Binutils/)和[GDB](https://unit-serow.github.io/2020/02/01/Debugger/)，因此BFD不单独发行，所以它通常包括在Binutils和GDB的发行之中

[^2]: 目标文件的结构:有一个有描述信息的“头”，可变量目的“段”，每个段都有一个名字，一些属性和一块数据，一个符号表，一组重定位入口顶等等
[^3]: 比如在小端序主机和大端序目标之间，在32-bit和64-bit数据之间的正确转换和重定位入口项所指定的寻址算术的细节
[^4]: 寻址是每种计算机中央处理器的指令集架构中的一部分，各个指令集下有不同的寻址模式，寻址模式决定了此架构下计算机语言指令所对应的运算数

---

**参考资料:**

参考网站-BFD的历史与故事[跳转](https://www.oreilly.com/openbook/opensources/book/tiemans.html)
`https://www.oreilly.com/openbook/opensources/book/tiemans.html`
