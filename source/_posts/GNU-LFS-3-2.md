---
title: GNU-LFS-3-2
date: 2020-03-01 00:58:18
tags: [随笔,GNU/Linux]
categories: [软件,GNU]
---

### GNU LFS-3-2

---

**目标主机-2**

* GCC
* Binutils
* LFS-v6.2/v6.3

---

### Binutils

**Binutils-2.17/Binutils-2.16.1**

> `$ tar xvf $LFS/binutils-2.17/2.16.1.tar.bz2`
> `$ mkdir -v ../binutils-build`
> `$ cd ../binutils-build`

* 编译配置:
```
$ ../binutils-2.17/2.16.1/configure --prefix=/usr \
		            --enable-shared
```

* 源码编译:
> `$ make tooldir=/usr`

**make参数含义:**
* 参数`tooldir=/usr`
> 通常情况下，tooldir(可执行文件的安装目录)是`$(exec_prefix)/$(target_alias)`
> 例如在i686机器上，将是`tt class="filename">/usr/i686-pc-linux-gnu`
> 因为此时只为自己的系统进 行编译，就并不需要在`/usr`目录后面再存在特殊的后缀
> `$(exec_prefix)/$(target_alias)`只是在交叉编译时(比如在Intel机器上编译将要在PowerPC上执行的程序)才用到

* 编译测试套件:
> `$ make check`

* 编译安装软件包
> `$ make tooldir=/usr install`

* 安装某些软件包需要的`libiberty头文件`
> `$ cp -v ../binutils-2.17/2.16.1/include/libiberty.h /usr/include`

* Binutils的内容这里不做过多阐述，可参考原文第6.11.2章节

---

### GCC-4.1.2/GCC-4.0.3

> `$ tar xvf $LFS/gcc-4.1.2/4.0.3.tar.bz2`
> `$ cd gcc-4.1.2/4.0.3`

* 先使用一个sed命令来禁止GCC安装它自己的`libiberty.a`
* 这里将使用Binutils附带的`libiberty.a`来代替
> `$ sed -i 's/install_to_$(INSTALL_DEST) //' libiberty/Makefile.in`

* 在临时主机中应用的bootstrap编译中，编译器会有`-fomit-frame-pointer`的标志
* 非bootstrap编译默认是忽略这个标志的，可以应用下面的sed命令来确保编译的可靠性
> `$ sed -i 's/^XCFLAGS =$/& -fomit-frame-pointer/' gcc/Makefile.in`

* `fixincludes脚本`偶尔会因为修改系统的头文件而出错
* 因为GCC-4.1.2/4.0.3和Glibc-2.5.1/2.3.6是不需要修改的，运行下面的命令可以避免`fixincludes脚本`运行:
> `$ sed -i 's@\./fixinc\.sh@-c true@' gcc/Makefile.in`

* GCC中提供了一个`gccbug脚本`，会在编译时侦测`mktemp`是否存在，并且在测试中加强代码
* 这将会导致脚本使用一些不算很随机的名字来命名临时文件
* 因为我们后面会安装mktemp	，这里就将人为的去模仿它的存在:
> `$ sed -i 's/@have_mktemp_command@/yes/' gcc/gccbug.in`

> `$ mkdir -v ../gcc-build`
> `$ cd ../gcc-build`

* 编译配置:
```
$ ../(gcc-4.1.2/4.0.3)/configure --prefix=/usr 	\ 
--libexecdir=/usr/lib 				\
--enable-shared 				\ 
--enable-threads=posix 				\
--enable-__cxa_atexit 				\ 
--enable-clocale=gnu 				\
--enable-languages=c,c++ 
```

* 参数作用与目标主机内的作用相同，这里不做过多阐述

> `$ make`

* 预编译测试:
> `$ make -k check`

> `$ make install`

* 有的软件包希望C PreProcessor(预处理器)安装在`/lib`目录下，为了满足它们的要求
* 需要创建如下符号链接:
> `$ ln -sv ../usr/bin/cpp /lib`

* 许多软件包使用cc作为C编译器的名字，为了满足它们的要求
* 需要创建如下符号链接:
> `$ ln -sv gcc /usr/bin/cc`

* 清理工作
> `$ cd ..`
> `$ rm -rf gcc-build`
> `$ rm -rf gcc-4.1.2`

---



