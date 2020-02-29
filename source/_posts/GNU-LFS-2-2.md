---
title: GNU-LFS-2-2
date: 2020-02-29 08:28:41
tags: []
categories: []
---

### GNU LFS-2-2

* 内容简述
> Linux Kernel Headeres(CN-LFS-6.2/6.3/9.0)
> Glibc/Libstdc++(CN-LFS-6.2/6.3/9.0)
> 第一遍的工具链调整(CN-LFS-6.2/6.3/9.0)

* 说明内容:
* 本篇内容将新版和旧版的资料相融合(将新版补充旧版的内容)
* 同时将其它的学习资料补充进LFS官方的文档内
* 在区分版本说明时，会先去介绍6.3再解释其它版本

---

### Linux API Headers 

* 每个版本的Linux kernel headers的名字都不一样

* 这里整合性的指出了三个版本的安装方法，分别是:
> Linux-2.6.22.5 API Headers(LFS-6.3)
> Linux-5.2.8 API (LFS-9.0)
> Linux-Libc-Headers-2.6.12.0 (LFS-6.2)

* 新建编译目录和清理工作这里就不做过多阐述了

---

**Version-2.6.22.5(LFS-v6.3)**

* 解压并进入文件夹
> `$ tar xvf /lfs-sources/linux-2.6.22.5.tar.bz2`
> `$ cd linux-2.6.22.5`

清除所有存在的多余依赖关系:
> `$ make mrproper` 

编译头文件
> `$ make headers_check`

* 从源代码中提取用户可见的内核头文件到指定位置
> `$ make INSTALL_HDR_PATH=dest headers_install`

* 保存在一个临时本地文件夹中然后复制到所需的位置
> `$ cp -rv dest/include/* /tools/include`

* 清理
> `$ cd ..`
> `$ rm -rf linux-2.6.22.5`

---

**Version-5.2.8(LFS-v9.0)**

* 大致构建用时: 0.1 SBU 
* 所需磁盘空间: 960 MB 

* 清除依赖项
> `$ make mrproper`

* 从源代码中提取用户可见的内核头文件
* 把它们保存在一个临时本地文件夹中然后复制到所需的位置
* 因为解压过程会移除目标文件夹中任何已有的文件
```
make INSTALL_HDR_PATH=dest headers_install
cp -rv dest/include/* /tools/include
```

---

**Version-2.6.12.0(LFS-未知版本)**

* Linux-Libc-Headers-2.6.12.0
* Linux-Libc-Headers内包含了纯净的内核头文件
* 预计编译时间：少于0.1
* SBU所需磁盘空间：27MB

* 安装这些头文件所需指令:
> `cp -Rv include/asm-i386 /tools/include/asm`
> `cp -Rv include/linux /tools/include`
* asm-i386为架构参数，需要自行进行调整

---

### Glibc

* Glibc-2.5.1
* Glibc-2.30

---

**Glibc-2.5.1**

* LFS-v6.3

* 解压并进入编译目录
```
$ tar xvf /lfs-sources/glibc-2.5.1.tar.bz2
$ mkdir -v glibc-build
$ cd glibc-build
```

* 编译配置
```
$ ../glibc-2.5.1/configure --prefix=/tools 	\
--disable-profile 				\
--enable-add-ons 				\
--enable-kernel=2.6.0 				\
--with-binutils=/tools/bin 			\	 
--without-gd 					\
--with-headers=/tools/include 			\ 
--without-selinux
```

**参数说明:**
* 参数`--prefix=/tools`
> 用于指定安装目录
* 参数`--disable-profile` 
* 参数`--enable-add-ons`
> 用于指示Glibc使用附加的NPTL包作为线程库
* 参数`--enable-kernel=2.6.0`
> 用于告诉Glibc编译支持2.6.x内核的库
* 参数`--with-binutils=/tools/bin`
> 用于保证在编译Glibc时不会用错Binutils程序
* 参数`--without-gd`
> 可以保证不生成memusagestat程序
* 参数`--with-headers=/tools/include` 
> 数指示Glibc按照前面刚刚安装到tools目录中的内核头文件编译自己
> 从而精确的知道内核的特性以根据这些特性对自己进行最佳化编译
* 参数`--without-selinux`
> 用于明确禁用含有SELinux特性的Glibc，以防止会出现许多操作失败的结果
* 其中参数`--enable-kernel=2.6.0`，只是为了说明kernel的大版本
> 所以不需要根据实际的kernel版本来改
> 即使是用linux-2.6.15也一样只写2.6.0就可以了

* 编译至二进制格式
> `$make`

* 配置链接器
> `$ mkdir -v /tools/etc`
> `$ touch /tools/etc/ld.so.conf`

* 编译安装
> `$ make install`

* 清理工作
> `$ cd ..`
> `$ rm -rf glibc-build`
> `$ rm -rf glibc-2.5.1`

---

**Glibc-2.30**

* Glibc 软件包包含了主要的 C 函数库
* 这个库提供了分配内存，搜索目录，打开关闭文件，读写文件，操作字 符串，模式匹配，基础算法等基本程序
* 大致构建用时: 4.8 SBU
* 所需磁盘空间: 896 MB 

* 编译配置
```
$ ../glibc-2.5.1/configure              \      
--prefix=/tools                    	\      
--host=$LFS_TGT                    	\      
--build=$(../scripts/config.guess) 	\      
--enable-kernel=3.2                	\      
--with-headers=/tools/include
```

**参数说明:**
* `$ --host=$LFS_TGT, --build=$(../scripts/config.guess)`
> 这些选项的组合效果是Glibc的构建系统配置它自己用`/tools`里面的交叉链接器和交叉编译器交叉编译自己
* `$ --enable-kernel=3.2`
> 这告诉Glibc编译能支持3.2以及之后的内核库
> 更早的内核版本不受支持
* `$ --with-headers=/tools/include`告诉Glibc利用刚刚安装在tools文件夹中的头文件编译自身
> 此能够根据内核的具体特性提供更好的优化 

* 在新版本的配置中，不仅需要安装C语言的标准库，还需要安装与配置对C++支持的标准库

* Libstdc++是标准的C++库
* 需要用它来编译C++ 代码(GCC的一部分是用C++写的)
* 但是在构建GCC Pass-1时，我们需要推迟它的安装进程，因为依赖的glibc，还未部署在`/tools`目录中
* 大致构建用时: 0.5 SBU
* 所需磁盘空间: 879 MB

* 记得新建源码编译目录与编译完清理，这里不对此部分进行赘述了
* 因为Libstdc++是GCC源文件的一部分
* 所以首先应该解压GCC的压缩包，然后进入`gcc-9.2.0`文件夹

* 编译配置
```
$ ../libstdc++-v3/configure             \    
--host=$LFS_TGT                 	\    
--prefix=/tools                 	\    
--disable-multilib              	\    
--disable-nls                   	\    
--disable-libstdcxx-threads     	\    
--disable-libstdcxx-pch         	\    
--with-gxx-include-dir=/tools/$LFS_TGT/include/c++/9.2.0
```

**配置说明:**

* 参数`--host=...`
> 用于指示使用我们刚才编译的交叉编译器，而不是`/usr/bin`中的
* 参数`--disable-libstdcxx-threads`
> 由于我们还没有编译C线程库，C++的也还不能编译
*  参数`--disable-libstdcxx-pch`
> 此选项防止安装预编译文件，此步骤并不需要
*  参数`--with-gxx-include-dir=/tools/$LFS_TGT/include/c++/9.2.0`
> 这是C++编译器搜索标准include文件的位置
> 在一般的编译中，这个信息自动从顶层文件夹中传入Libstdc++ configure选项
> 在我们的例子中，必须明确给出这信息

* 进行编译安装
> $ make
> $ make install

---

**其它情况**

* 在编译过程中可能会发生以下警告

```
configure: WARNING: 
*** These auxiliary programs are missing or 
*** incompatible versions: msgfmt 
*** some features will be disabled. 
*** Check the INSTALL file for required versions.
```

* msgfmt程序的缺失或者不兼容通常是无害的
* 这个msgfmt程序是Gettext软件包的一部分，主机发行版应该提供了

---

### 调整工具链

* 根据自身情况进行工具链调整
* 以下实例为LFS-v6.3的配置代码
* 同时也包括了部分LFS-v6.2的内容

---

**调整思路:**
* 因为现在临时的C库已经装好，接下来本章中要编译的所有工具应该连接到这些库上
* 为了达到这个目标，需要调整连接器和编译器的specs文件
* 在第一遍编译Binutils快结束时已经调整过的连接器，现在需要被重新命名以便可以被正确的找到和使用
* 首先备份原来的连接器，然后用调整过的连接器来替代
* 最后还要创建一个指向`/tools/$(gcc-dumpmachine)/bin`中连接器副本的连接
* 如果当前本地主机的系统平台上，动态连接器的名字不是`ld-linux.so.2`
* 必须人为的把spaces配置里的`ldlinux.so.2`换成你的系统平台上动态连接器的名字

---

* 以下为工具链配置代码(LFS-6.3)
```
$ mv -v /tools/bin/{ld,ld-old} 
$ mv -v /tools/$(gcc -dumpmachine)/bin/{ld,ld-old} 
$ mv -v /tools/bin/{ld-new,ld} 
$ ln -sv /tools/bin/ld /tools/$(gcc -dumpmachine)/bin/ld 
$ gcc -dumpspecs | sed 's@^/lib/ld-linux.so.2@/tools&@g' > `dirname $(gcc -print-libgcc-file-name)`/ specs 
$ GCC_INCLUDEDIR=`dirname $(gcc -print-libgcc-file-name)`/include && 
find ${GCC_INCLUDEDIR}/* -maxdepth 0 -xtype d -exec rm -rvf '{}' \; && 
rm -vf `grep -l "DO NOT EDIT THIS FILE" ${GCC_INCLUDEDIR}/*` &&
unset GCC_INCLUDEDIR
```

**语句内容刨析:**

* 符号链接部分

```
$ mv -v /tools/bin/{ld,ld-old} 
$ mv -v /tools/$(gcc -dumpmachine)/bin/{ld,ld-old} 
$ mv -v /tools/bin/{ld-new,ld} 
$ ln -sv /tools/bin/ld /tools/$(gcc -dumpmachine)/bin/ld
```
* 就是几个符号链接
* 当设置完成之后，所有程序都将连接到`/tools/lib`中的库文件

* space部分

```
$ gcc -dumpspecs | sed 's@^/lib/ld-linux.so.2@/tools&@g' > `dirname $(gcc -print-libgcc-file-name)`/ specs 
$ GCC_INCLUDEDIR=`dirname $(gcc -print-libgcc-file-name)`/include && 
find ${GCC_INCLUDEDIR}/* -maxdepth 0 -xtype d -exec rm -rvf '{}' \; && 
rm -vf `grep -l "DO NOT EDIT THIS FILE" ${GCC_INCLUDEDIR}/*` &&
unset GCC_INCLUDEDIR
```
此代码还可以拆成以下两部分

* 部分一
```
$ SPECFILE=`dirname $(gcc -print-libgcc-file-name)`/specs && 
gcc -dumpspecs > $SPECFILE &&
sed 's@^/lib/ld-linux.so.2@/tools&@g'	$SPECFILE > tempspecfile &&
mv -vf tempspecfile $SPECFILE && 
unset SPECFILE
```
* 用于修正GCC的specs文件，使它指向新的动态连接器
* 只需要像以上那样使用一个简单的sed命令就能做到
* 同时也可以手动编辑specs文件
> 本质上就是把所有的`/lib/ld-linux.so.2`都替换成`/tools/lib/ld-linux.so.2`就行

* 部分二
```
$ GCC_INCLUDEDIR=`dirname $(gcc -print-libgcc-file-name)`/include &&
find ${GCC_INCLUDEDIR}/* -maxdepth 0 -xtype d -exec rm -rvf '{}' \; &&
rm -vf `grep -l "DO NOT EDIT THIS FILE" ${GCC_INCLUDEDIR}/*` &&
unset GCC_INCLUDEDIR
```
* 用于删除GCC专属头文件目录中的头文件
> 以避免宿主系统中的头文件污染编译环境

---

* 相关说明
> 工具链的调整方法有好几种，而且不同版本GCC的specs可能会有不同
> 但实际上都是把specs文件中的`/lib/ld-linux.so.2`替换成了`/tools/lib/ld-linux.so.2`
> 所以即使有些文章在调整工具链上的命令和LFS手册上的不一样也不用太奇怪
> 当然也可以 直接用`gcc -dumpspecs`导出后手工直接编辑specs文件
> spaces必须加以检查以确保被修改的配置的的确确生效了

---

### 内容参考

* CN-LFS-v9.0
* CN-LFS-v6.3
* CN-LFS-v6.2
* 在LFS-1的URL资源整合目录里都有说明

---



