---
title: GNU-LFS-2-1
date: 2020-02-29 01:06:14
tags: [随笔,GNU/Linux]
categories: [软件,GNU]
---

## GNU LFS-2-1

---

### 构造临时系统-1.0

*  1.0-为第一遍编译并安装临时工具链内Binutils与GCC

**概述:**
* 对于临时系统的简述
* 目的是何构造一个最小的Linux系统
* 该系统将包含刚好足够构建目标主机中最终LFS系统所需的工具，以及一个比最小环境具有更好用户便利性的工作环境
* 使用的软件包皆为v6.3版本的LFS-liveCD中拥有的软件包
* 本文只介绍基本的[GNU 工具链]的搭建参考于v6.3与v9.0(对6.3进行补充，对9.0进行说明)
> v6.3和v9.0都有进行举例说明

* 构建这个最小系统有两个步骤:
> 第一步: 构建一个与宿主系统无关的新工具链(编译器、汇编器、链接器、 库和一些有用的工具)
> 第二步: 使用该工具链，去构建其它的基础工具

* 临时系统中编译得到的文件将被安装在目录`$LFS/tools`中
> 以确保在下一章中安装的文件和宿主系统生成的目录相互分离
> 由于此处编译的软件包都是临时性的，因此可以人为的去避免出现污染后面即将构成的LFS系统的情况发生

**需要特别注意的几点:**
* 在构建的过程需要注意的问题
1. 把所有源文件和补丁放到 chroot 环境可访问的目录，例如`/mnt/lfs/sources/`
> 但是千万不 能把源文件放在`/mnt/lfs/tools/`中
2. 进入到源文件目录
3. 对于每个软件包: 
> a. 用tar程序解压要编译的软件包
> 同时在临时系统目录中，确保解压软件包时本地主机使用的是lfs用户
> b. 进入到解压后创建的目录中
> c. 根据指南说明编译软件包
> d. 回退到源文件目录
> e. 除非特别说明，删除解压出来的目录
 
---

* 进入LFS包编译目录
> `cd $LFS/sources`

* 第一遍编译[GNU 工具链]说明:
> 在编译完成之后，通常需要运行测试套件
> 但此时测试套件框架(Tcl，Expect和DejaGNU)还没有就绪
> 同时因为此时是所有工作的初期阶段
> 所以此进行测试的收效甚微，因为第一遍编译的程序很快会被第二遍的代

---

### 1.0.0

**Binutils-2.17/2.32-Pass 1**
**安装交叉编译的Binutils**

* 目标软件包简述:
> Binutils 软件包包含一个链接器，一个汇编器，以及其它处理目标文件的工具
> 大致构建用时: 1 SBU
> 所需磁盘空间: 580 MB

* 创建目录
```
$ tar xvf /lfs-sources/binutils-2.17.tar.bz2
$ mkdir -v binutils-build
$ cd binutils-build
```

* v6.3配置编译
```
CC="gcc -B/usr/bin/" ../binutils-2.17/configure --prefix=/tools  	\
				            --disable-nls 		\
				            --disable-werror 
```

* v9.0编译配置
```
$ CC="gcc -B/usr/bin/"  ../binutils-2.32/configure 	--prefix=/tools            \
             					--with-sysroot=$LFS        	\
             					--with-lib-path=/tools/lib 	\
             					--target=$LFS_TGT          	\
             					--disable-nls              	\
             					--disable-werror
```

**参数说明:**

* 参数`CC="gcc -B/usr/bin/"`该选项强制gcc使用宿主系统中/usr/bin目录下的连接器
> 这样做的必要是因为新生成的ld可能与某些宿主系统的gcc不兼容
* 参数`--prefix=/tools`用于告诉配置脚本将`Binutils程序`安装到`/tools`文件夹
* 参数`--with-sysroot=$LFS`用于交叉编译，告诉编译系统在`$LFS`中查找所需的目标系统库
* 参数`--with-lib-path=/tools/lib`指定需要配置使用的链接器的库路径
* 参数`--target=$LFS_TGT`，因为`LFS_TGT`变量中的机器描述和`config.guess`脚本返回的值略有不同，这个选项会告诉`configure`脚本调整`Binutils`的构建系统来构建一个交叉链接器
* 参数`--disable-nls`会禁止国际化(i18n)，因为国际化对临时工具来说没有必要
* 参数`--disable-werror`会防止来自宿主编译器的警告事件导致停止编译 

* 继续编译并进行编译安装
> $make
> $make install

* 为调整工具链步骤准备连接器
```
$ make -C ld clean 
$ make -C ld LIB_PATH=/tools/lib
$ cp -v ld/ld-new /tools/bin
```

**参数说明:**
* 参数`-C ld clean`
> 用于告诉make程序删除所有ld子目录中编译生成的文件
* 参数`-C ld LIB_PATH=/tools/lib`
> 用于这个选项重新编译ld子目录中的所有文件

* 清理工作
```
$ cd .. 
$ rm -rf binutils-build
$ rm -rf binutils-2.17
```

* 如果是在`x86_64`上构建，创建符号链接，以确保工具链的完整性:
```
$ case $(uname -m) in  
	x86_64) mkdir -v /tools/lib && ln -sv lib /tools/lib64 ;; 
esac
```

* 该软件包的详细信息位于`Section#6.16.2`的`Binutils内容`

---

### 2.0.0

**GCC-4.12/9.2.0 Pass-1**
**安装交叉编译的GCC**

* 目标软件包简述:
> GCC软件包包括GNU编译器集，其中有C和C++的编译器
> 大致构建用时: 12 SBU
> 所需磁盘空间: 3.1 GB 

**以下内容为LFS-v6.3的GCC编译过程**
* 创建目录
```
$ tar xvf /lfs-sources/gcc-4.1.2.tar.bz2
$ mkdir -v gcc-build
$ cd gcc-build
```

* v6.3编译配置
```
CC="gcc -B/usr/bin/" ../gcc-4.1.2/configure 	--prefix=/tools 		\ 
				      		 --with-local-prefix=/tools 	\
				       		--disable-nls 			\
				       		--enable-shared 		\
				       		--enable-languages=c 
```

* v9.0编译配置
```
CC="gcc -B/usr/bin/" ../gcc-9.2.0/configure       	\
 --target=$LFS_TGT                              	\
 --prefix=/tools                                	\ 
 --with-glibc-version=2.11                      	\ 
  --with-sysroot=$LFS                            	\ 
  --with-newlib                                  	\ 
 --without-headers                              	\ 
 --with-local-prefix=/tools                     	\ 
 --with-native-system-header-dir=/tools/include 	\ 
 --disable-nls                                  	\
 --disable-shared                               	\
 --disable-multilib                             	\ 
 --disable-decimal-float                        	\ 
 --disable-threads                              	\ 
 --disable-libatomic                            	\ 
 --disable-libgomp                              	\ 
 --disable-libquadmath                          	\ 
 --disable-libssp                               	\ 
 --disable-libvtv                               	\
 --disable-libstdcxx                            	\ 
 --enable-languages=c,c++
```

---
**配置含义(参数说明):**

* 参数`--with-newlib`
> 由于还没有可用的C库，这确保编译libgcc时定义了常数`inhibit_libc`
> 这可以防止编译任何需要libc支持的代码
* 参数`--without-headers`
> 在创建完整的交叉编译器时，GCC要求标准头文件和目标系统兼容
> 对于我们的目的来说，不需要这些头文件
> 这个选项可以防止GCC查找它们
* 参数`--with-local-prefix=/tools GCC`
> 此参数会查找本地已安装的include文件的系统位置
> 默认是`/usr/local`
> 把它设置为`/tools`能把主机位置中的`/usr/local`从GCC的搜索路径中排除
* 参数`--with-native-system-header-dir=/tools/include`
> GCC默认会在/usr/include中查找系统头文件
> 和`sysroot`选项一起使用，会转换为`$LFS/usr/include`
> 在后面两个章节中头文件会被安装到`$LFS/tools/include`
> 这个选项确保 gcc 能正确找 到它们
> 第二次编译 GCC 时，同样的选项可以保证不会去寻找主机系统的头文件
* 参数`--disable-shared`
> 这个选项强制GCC静态链接到它的内部库
> 我们这样做是为了避免主机系统可能出现的问题
* 参数:
> `--disable-decimal-float`,`--disable-threads`,`--disable-libatomic`,`--disablelibgomp`,
> `--disable-libquadmath`,`--disable-libssp`,`--disable-libvtv`,`--disablelibstdcxx`
> 这些选项取消了对十进制浮点数扩展，线程化，`libatomic`，`libgomp`，`libquadmath`，`libssp`，`libvtv`，`libcilkrts`和`C++`标准库的支持
> 这些功能在编译 交叉编译器的时候会导致编译失败，对于交叉编译临时 libc 来说也没有必要
* 参数`--disable-multilib`
> 在`x86_64`机器上，LFS 还不支持`multilib`配置
> 这个选项对 x86 来说无害
* 参数`--enable-languages=c,c++`
> 这个选项确保只编译 C 和 C++ 编译器
> 这些是现在唯一需要的语言
* 此时只编译了GCC里的C编译器
---

* 编译并安装
```
> $ make bootstrap
> $ make install 
```

* 创建符号连接(工具链)
> `$ ln -vs gcc /tools/bin/cc`

* 清理工作
```
$ cd .. 
$ rm -rf gcc-build 
$ rm -rf gcc-4.1.2
```

* 该软件包的详细信息位于`Section#6.21.2`的GCC软件包内容里

---

* 对于工具链内的工具或其它软件的编译安装大致可分为以下几步:
1. 创建目录
2. 配置编译器与其脚本文件
3. 编译并安装
4. 配置工具链
* 配置其它独有(针对于不同工具的特殊配置)性质

---

### 参考资料

* 金钟国的v6.3-LFS
* 孙海勇的v6.3-LFS
* LFS-v9.0

* `5.4. Binutils-2.18 - 第一遍`[跳转](https://blbl.dev/lfs_6.4_zhcn/chapter05/binutils-pass1.html)
> `https://blbl.dev/lfs_6.4_zhcn/chapter05/binutils-pass1.html`
* `gcc -B/usr/bin -B`的含义[跳转](https://www.169it.com/tech-qa-linux/article-10702497996978005026.html)
> `https://www.169it.com/tech-qa-linux/article-10702497996978005026.html`
* 百度知道[跳转](https://zhidao.baidu.com/question/501313846.html)
> `https://zhidao.baidu.com/question/501313846.html`

---



