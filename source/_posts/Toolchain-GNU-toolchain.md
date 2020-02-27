---
title: Toolchain/GNU toolchain
date: 2020-02-27 21:08:35
tags: [GNU/Linux,随笔]
categories: [软件,GNU]
---

## 工具链基本概念简述-1

* 此模块只做简单的概述与对于概念的浅层理解
* 工具环境所需要的包这里不做过多赘述(与工具链无关)

---

### 工具链

**概述:**
* Toolchain
* 在开发软件过程中，一组工具链(toolchain)是一系列用于制作软件程序的工具
* 这些工具一般一个接一个地运用，上一个工具的输出即是下一个工具的输入，因此得名
* 但工具链这个词汇也可指涉这些工具并无此相依运行的限制
* 工具链与集成开发环境形成对照，分别代表了两种不同风格的软件开发环境

**基本构成:**
* 通常一个软件开发的工具链由以下组成:
1. 编译器
2. 链接器 (将源代码/目标代码转换成可执行程序档)
3. 库 (提供与操作系统之间的界面)
4. 调试器 (用来测试、调试所产出的程序)

---

### GNU 工具链

**概述:**
* GNU toolchain
* 是一个包含了由GNU计划所产生的各种编程工具的集合，由自由软件基金会负责维护工作
* 这些工具形成了一条工具链，用于开发应用程序和操作系统
* 同时与集成开发环境相对应

**GNU工具链组成:**

* GNU make：用于编译和构建的自动工具
* GNU编译器集合 (GCC) 一组多种编程语言的编译器
* GNU Binutils: 包含链接器、汇编器和其它工具的工具集
* GNU Bison: 编译器编译程序，经常和 Flex词法分析器 配合使用
* GNU m4: m4 宏预处理器
* GNU Debugger (GDB):代码调试工具
* GNU构建系统 (autotools):
> Autoconf
> Autoheader
> Automake
> Libtool
* GNU C Library: GNU C标准函数库
* GNU Classpath

---

### 交叉工具链:

**概述:**
* 用于提供编译，链接，处理等功能
* 就是为了编译，链接，处理和调试跨平台体系结构的程序代码
* 每次执行工具链软件时，通过带有不同的参数，可以实现编译，链接，处理或者调试等不同的功能
* 从工具链的组成上来说，它一般由多个程序构成，分别对应着各个功能

* 所谓的交叉工具链是由以下两个概念组合而成的:
1. 交叉编译: 是A机器上编译生成，运行在B机器上
> 两个机子有不同的机器指令
2. 工具链: 一般由编译器，连接器，解释器和调试器组成

---

### 交叉编译器:

* 是指一个在某个系统平台下可以产生另一个系统平台的可执行文件的编译器
* 交叉编译器在目标系统平台(开发出来的应用程序序所运行的平台)难以或不容易编译时非常有用
* 交叉编译器的存在对于从一个开发主机为多个平台编译代码是非常有必要的
* 直接在平台上编译有时行不通，例如在一个嵌入式系统的单片机 ，因为它们没有操作系统，所以直接编译行不通
* 交叉编译器和源代码至源代码编译器不同，交叉编译器用于二进制代码的跨平台软件开发
> 而源到源编译器是将某种编程语言的程序源代码作为输入
> 生成以另一种编程语言构成的等效源代码的编译器，但两者都是编程工具
* 交叉编译器的基本用法就是将构建环境与目标环境分开
* 常在下面几种情况中使用(具体使用方法这里不做过多赘述):
> 嵌入式电脑
> 编译多个目标库
> 引导一个新平台(Bootstrapping)
> 程序虚拟机(比如JVM)

---

* 工具链用途简述:
* GNU工具链在针对嵌入式系统的Linux内核、BSD及其它软件的开发中起着至关重要的作用
* GNU工具链中的部分工具也被Solaris, Mac OS X, Microsoft Windows (via Cygwin and MinGW/MSYS) and Sony PlayStation 3等其它平台直接使用或进行了移植

---

**工具链相关概念(关键字):**
* 工具链
* GNU 工具链
* 集成开发环境
* 编译器/标准库/链接器/调试器
* 交叉编译器
* 分布式/并发版本控制系统(CVS,Git等等)
* 工具链环境

---

## 补充内容

**工具链环境:**

* 所谓的工具链环境就是:
> 不光包含于工具链的基本组件
> 还包含于各类辅助指令所对应的工具与程序的本地系统环境

---

### GNU工具链组件完全性参考:

**基本工具:**

* GNU make: 用于编译和构建的自动工具
* GNU编译器集(GCC): 一组多种编程语言的编译器
* GNU Binutils: 包含链接器，汇编器和其它工具的工具集
* GNU调试工具(GDB): 代码调试工具
* GNU自动化生成工具(autotools): 自动化检查软件编译过程的工具

---

**工具链体系:**

* 此部分用于描述工具链的相关概念与结构，以实现对工具链实施完整的分析
* 本文选取LFS的工具链来说明工具链体系内的软件包组成及依赖关系
* 为了使以上不同类别的所属工具形成一个互相关联且互相依赖的工具链体系
* 必须安装与配置以下软件包工具与相关程序及源码来构成与实现其工具链体系的依赖关系

**所需软件一览:**

**Binutils(汇编器):**
* 包含的程序: 
> `addr2line，ar，as，c++filt，elfedit，gprof，ld，ld.bfd`，
> `nm，objcopy，objdump，ranlib，readelf，size，strings 和 strip`
* 包含的库: 
> `libiberty，libbfd` 和 `libopcodes`

**GCC(编译器):**
* 包含的程序: 
> `c++，cc(到 gcc 的链接)，cpp，g++，gcc`，
> `gcc-ar，gcc-nm，gcc-ranlib，gccbug` 和 `gcov`
* 包含的库: 
> `libgcc，libgcov，libgomp，liblto_plugin，libmudflap`，
> `libquadmath，libssp，libstdc++，libsupc++`
* 依赖的包: `gmp，mpfr，mpc`

**Linux API Headers:**
* 这个是可选包，如果是为了做一个通用工具链，必须将其换成相应平台的头文件包
* 包含的头文件:
>  `/usr/include/asm/*.h`，`/usr/include/asm-generic/*.h`，
> `/usr/include/drm/*.h`，`/usr/include/linux/*.h`，`/usr/include/mtd/*.h`，
> `/usr/include/rdma/*.h`，`/usr/include/scsi/*.h`，
> `/usr/include/sound/*.h`，`/usr/include/video/*.h`，`/usr/include/xen/*.h`

**Glibc:**
* 可以根据标准LFS系统的制作方法来安装Glic(可以大幅度简化实现难度)
* 包含的程序: 
> `catchsegv，gencat，getconf，getent，iconv，iconvconfig`，
> `ldconfig，ldd，lddlibc4，locale, localedef，makedb，mtrace，nscd`，
> `pcprofiledump，pldd，pt_chown，rpcgen, sln, sotruss, sprof, tzselect, xtrace, zdump 和 zic`
* 包含的库:
> `ld.so`，`libBrokenLocale`，`libSegFault`，`libanl`，`libbsd-compat`，`libc`，`libcidn`，`libcrypt`，
> ` libdl`，`libg`，`libieee`，`libm`，`libmcheck`，`libmemusage`，`libnsl`，`libnss`，`libpcprofile`，`libpthread`，
> `libresolv`，`librpcsvc`，`librt`，`libthread_db`，`libutil`

---

### 参考资料

* CN-WIKI GNU核心工具组[跳转](https://zh.wikipedia.org/wiki/GNU%E6%A0%B8%E5%BF%83%E5%B7%A5%E5%85%B7%E7%BB%84)
> `https://zh.wikipedia.org/wiki/GNU%E6%A0%B8%E5%BF%83%E5%B7%A5%E5%85%B7%E7%BB%84`

* CN-WIKI GNU工具链[跳转](https://zh.wikipedia.org/wiki/GNU%E5%B7%A5%E5%85%B7%E9%93%BE)
> `https://zh.wikipedia.org/wiki/GNU%E5%B7%A5%E5%85%B7%E9%93%BE`

* CN-WIKI 交叉工具链[跳转](https://zh.wikipedia.org/wiki/%E4%BA%A4%E5%8F%89%E7%B7%A8%E8%AD%AF%E5%99%A8)
> `https://zh.wikipedia.org/wiki/%E4%BA%A4%E5%8F%89%E7%B7%A8%E8%AD%AF%E5%99%A8`

* 百度百科 交叉工具链[跳转](https://baike.baidu.com/item/%E4%BA%A4%E5%8F%89%E5%B7%A5%E5%85%B7%E9%93%BE/2503696)
> `https://baike.baidu.com/item/%E4%BA%A4%E5%8F%89%E5%B7%A5%E5%85%B7%E9%93%BE/2503696`

* CN-WIKI 交叉编译器[跳转](https://zh.wikipedia.org/wiki/%E4%BA%A4%E5%8F%89%E7%B7%A8%E8%AD%AF%E5%99%A8)
> `https://zh.wikipedia.org/wiki/%E4%BA%A4%E5%8F%89%E7%B7%A8%E8%AD%AF%E5%99%A8`

* Linux From Scratch (简体中文版/版本: 9.0)[跳转](https://lctt.github.io/LFS-BOOK/lfs-sysv/LFS-BOOK.pdf)
> Chapter (5.x. 构建临时系统) 与 (5.2. 工具链技术说明)
> `https://lctt.github.io/LFS-BOOK/lfs-sysv/LFS-BOOK.pdf`

* 工具链技术分析与实现(GNU 工具链)[跳转](https://www.cnblogs.com/Leo_wl/p/3405580.html)
> `https://www.cnblogs.com/Leo_wl/p/3405580.html`


---

## 补充内容

### 工具链技术实现

* GNU 工具链

### 工具链的使用方式

* 工具链的目的是提供一个临时可用的编译工作环境，通过chroot来完成在工具环境中进行开发、编译、制作工作
* 为了制作出干净、可移植的工具环境，建议创建一个专用于制作工具链的用户，这也是LFS推荐的

* 在使用工具链之前，此时的本地环境身份应该是root
* 首先挂载虚拟文件系统，然后进入到chroot环境中

1. **挂载虚拟文件系统**

* 可以将以下代码保存为相应的Shell脚本文件，添加执行权限即可使用
* 使用顺序是先挂载虚拟文件系统、后进入chroot环境

* 下方代码只适用于LFS的构建，可根据需求做适当的变量替换，原理和步骤是相同的
```
#!/bin/bash

mount -o bind /dev $LFS/dev
mount -t devpts devpts $LFS/dev/pts -o gid=5,mode=620
mount -t proc proc $LFS/proc
mount -t sysfs sysfs $LFS/sys

if [ -h $LFS/dev/shm ]; then
  link=$(readlink $LFS/dev/shm)
  mkdir -p $LFS/$link
  mount -t tmpfs shm $LFS/$link
  unset link
else
  mount -t tmpfs shm $LFS/dev/shm
fi
```

2. 进入到Chroot环境执行以下代码:

```
#!/bin/bash

chroot "$LFS" /tools/bin/env -i \
    HOME=/root                  \
    TERM="$TERM"                \
    PS1='\u:\w\$ '              \
    PATH=/tools/bin:/tools/sbin:/bin:/usr/bin:/sbin:/usr/sbin \
    /tools/bin/bash --login +h
```

---

* Linux From Scratch (简体中文版/版本: 9.0)[跳转](https://lctt.github.io/LFS-BOOK/lfs-sysv/LFS-BOOK.pdf)
> Chapter (5.x. 构建临时系统) 与 (5.2. 工具链技术说明)
> `https://lctt.github.io/LFS-BOOK/lfs-sysv/LFS-BOOK.pdf`

* 工具链技术分析与实现(GNU 工具链)[跳转](https://www.cnblogs.com/Leo_wl/p/3405580.html)
> `https://www.cnblogs.com/Leo_wl/p/3405580.html`

---



