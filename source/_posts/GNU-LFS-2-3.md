---
title: GNU-LFS-2-3
date: 2020-02-29 19:22:36
tags: [GNU/Linux,随笔]
categories: [软件,GNU]
---

### GNU LFS-2.3

* GCC Pass-2
* Bintils Pass-2

---

### Bintils Pass-2

* Binutils-2.16.1/LFS-6.2 Pass-2 154 MB 1.1 SBU
* Binutils-2.17/LFS-6.3 Pass 2
* Binutils-2.32/LFS-9.0 Pass-2 879 MB 1.1 SUB

---

**Binutils-2.16.1/2.17**

* 解压文件并进入编译目录
```
$ tar xvf /lfs-sources/binutils-2.17.tar.bz2 
$ mkdir -v binutils-build
$ cd binutils-build
```

编译配置
```
$ ../binutils-2.17(-2.16.1)/configure --prefix=/tools 	\
			--disable-nls 		\ 
			--with-lib-path=/tools/lib 
```

* 新参数含义:
* 参数`--with-lib-path=/tools/lib`
> 这个选项指示configure脚本在Binutils编译过程中将传递给连接器的库搜索路径设为`/tools/lib`
> 以防止连接器搜索宿主系统的库目录

* 编译及安装
> `$ make`
> `$ make install`

* 为目标机器的工具链调整配置连接器
```
$ make -C ld clean 
$ make -C ld LIB_PATH=/usr/lib:/lib 
$ cp -v ld/ld-new	/tools/bin
```

* 最后清理一下
> `$ cd .. rm -rf binutils-build` 
> `$ rm -rf binutils-2.17`

---

**Binutils-2.32**

* 编译配置
```
$ CC=$LFS_TGT-gcc                \ 
AR=$LFS_TGT-ar                	 \ 
RANLIB=$LFS_TGT-ranlib        	 \ 
../configure                	 \    
--prefix=/tools         	 \    
--disable-nls            	 \    
--disable-werror       		 \   
--with-lib-path=/tools/lib 	 \  
 --with-sysroot
```

**参数含义:**
* 参数`CC=$LFS_TGT-gcc`,`AR=$LFS_TGT-ar`,`RANLIB=$LFS_TGT-ranlib`
> 因为这是真正的原生编译Binutils，设置这些变量能确保编译系统使用交叉编译器和相关的工具，而不是 宿主系统中已有的
* 参数`--with-lib-path=/tools/lib` 
> 这告诉配置脚本在编译Binutils的时候指定库搜索目录，此处将`/tools/lib`传递到链接器
* 参数`--with-sysroot sysroot`
> 功能使链接器可以找到包括在其命令行中的其它共享对象明确需要的共享对象
> 否则的话，在某些主机上一些软件包可能会编译不成功

* 之后进行编译安装

* 为目标机器中的工具链阶段准备链接器
```
$ make -C ld clean 
$ make -C ld LIB_PATH=/usr/lib:/lib 
$ cp -v ld/ld-new /tools/bin
```

**make 参数说明**

* 参数`-C ld clean`
> 用于告诉make程序移除所有ld子目录中编译过的文件
* 参数`-C ld LIB_PATH=/usr/lib:/lib`
> 这个选项重新编译ld子目录中的所有文件
> 在命令行中指定`Makefile`的`LIB_PATH`变量可以使我们能 够重写临时工具的默认值并指向正确的最终路径
>该变量的值指定链接器的默认库搜索路径
> 目标主机中会用到这个准备 

---

### GCC Pass-2

* GCC 9.2.0 LFS-9.0 3.7 GB/15 SBU
* GCC 4.1.2 LFS-6.3
* GCC 4.0.3 LFS-6.2 443 MB/4.2 SBU

---

**GCC 4.1.2/4.0.3 Pass-2**

> `$ tar xvf /lfs-sources/gcc-4.1.2.tar.bz2`
> `$ cd gcc-4.1.2`

* 禁止fixincludes脚本运行，以保证编译环境不被污染
> `$ cp -v gcc/Makefile.in{,.orig}`
> `$ sed 's@\./fixinc\.sh@-c true@' gcc/Makefile.in.orig > gcc/Makefile.in`
* 因为在之前的`GCC Pass-1`中进行的`bootstrap`编译使用了`-fomit-frame-pointer`选项，而非bootstrap`编译则默认忽略了该选项
* 所以需要使用下面的sed命令来确保在非`bootstrap`编译时也同样使用`-fomit-frame-pointer`选项，以保持一致性
> `$ cp -v gcc/Makefile.in{,.tmp}`
> `$ sed 's/^XCFLAGS =$/& -fomit-frame-pointer/' gcc/Makefile.in.tmp gcc \`
> `> Makefile.in`
* 使用下面的补丁来修改GCC的缺省动态连接器(通常是`ld-linux.so.2`)的位置，同时把`/usr/include`从GCC的头文件搜索路径里删掉:
> `$ patch -Np1 -i /lfs-sources/gcc-4.1.2-specs-1.patch `
* 预先打补丁而不是在安装GCC之后调整specs文件的作用是:
> 可以保证新的动态连接器在编译GCC的时候就用上
> 也就是说，随后的所有临时程序都会连接到新的Glibc上
* 此补丁非常重要，必须进行使用才能成功编译


* GCC Pass-2 编译配置:
```
$ mkdir -v ../gcc-build
$ cd ../gcc-build 
$ ../gcc-4.1.2/configure --prefix=/tools 	\ 
--with-local-prefix=/tools 			\ 
--enable-clocale=gnu 				\
--enable-shared 				\ 
--enable-threads=posix 				\
--enable-__cxa_atexit 				\ 
--enable-languages=c,c++ 			\
--disable-libstdcxx-pch
```

**参数解析:**
`--prefix=/tools`
`--with-local-prefix=/tools`
* 参数`--enable-clocale=gnu`
> 用于确保确保C++库在任何情况下都使用正确的locale模块
* 参数`--enable-threads=posix`
> 用于使C++异常能处理多线程代码
* 参数`--enable-__cxa_atexit`
> 用`__cxa_atexit`代替`atexit`来登记C++对象的本地静态和全局析构函数
> 这是为了完全符合标准对析构函数的处理规定
* 参数`--enable-languages=c,c++`
> 用于编译C和C++语言的编译器
* 参数`--disable-libstdcxx-pch`
> 不为`libstdc++`编译预编译头(PCH)，它占用了很大空间，并且在此版本中用不到它

---

**编译安装并清理:**
> `$ make`
> `$ make install`
> `$ cd ..`
> `$ rm -rf gcc-build`
> `$ rm -rf gcc-4.1.2`

---

**GCC 9.2.0 Pass-2**

* 因为在第一次编译GCC的时候安装了一些内部系统头文件
* 其中的一个`limits.h`会反过来包括对应的系统头文件`limits.h`，在本次的实例中，是`/tools/include/limits.h`
* 但是，第一次编译gcc的时候`/tools/include/limits.h`并不存在
* 因此GCC安装的内部头文件只是部分的自包含文件，并不包括系 统头文件的扩展功能
* 这足以编译临时libc，但是这次编译GCC要求完整的内部头文件
* 使用和正常情况下GCC编译系统使用的相同的命令创建一个完整版本的内部头文件:
```
$ cat gcc/limitx.h gcc/glimits.h gcc/limity.h > \  
`dirname $($LFS_TGT-gcc -print-libgcc-file-name)`/include-fixed/limits.h 
```

* 再一次更改 GCC 的默认动态链接器的位置，使用安装在`/tools`的那个
* 执行以下配置:
```
$ for file in gcc/config/{linux,i386/linux{,64}}.h 
do  
cp -uv $file{,.orig}  
sed -e 's@/lib\(64\)\?\(32\)\?/ld@/tools&@g' \
       -e 's@/usr@/tools@g' $file.orig > $file  
echo ' 
#undef STANDARD_STARTFILE_PREFIX_1 
#undef STANDARD_STARTFILE_PREFIX_2 
#define STANDARD_STARTFILE_PREFIX_1 "/tools/lib/" 
#define STANDARD_STARTFILE_PREFIX_2 ""' >> $file  
touch $file.orig 
done 
```

* 如果是在`x86_64`环境上构建，为64位库改变默认目录名至`lib`:
```
case $(uname -m) in  
x86_64)    
sed -e '/m64=/s/lib64/lib/' \        
-i.orig gcc/config/i386/t-linux64  
;; 
esac
```

* 和第一次编译GCC一样，它要求GMP,MPFR和MPC软件包
* 解压tar包并把它们重名为到所需的文件夹名
* 执行以下命令:
```
$ tar -xf ../mpfr-4.0.2.tar.xz 
$ mv -v mpfr-4.0.2 mpfr 
$ tar -xf ../gmp-6.1.2.tar.xz 
$ mv -v gmp-6.1.2 gmp 
$ tar -xf ../mpc-1.1.0.tar.gz 
$ mv -v mpc-1.1.0 mpc 
```

---

* 在开始编译 GCC 之前，注意要取消所有会覆盖默认优化选项的环境变量

* 编译配置:
```
$ CC=$LFS_TGT-gcc                                   	\ 
CXX=$LFS_TGT-g++                               		\ 
AR=$LFS_TGT-ar                                 		\ 
RANLIB=$LFS_TGT-ranlib                             	\ 
../configure                                      	\    
--prefix=/tools                                		\	    
--with-local-prefix=/tools                 		\    
--with-native-system-header-dir=/tools/include    	\    
--enable-languages=c,c++                                \    
--disable-libstdcxx-pch                       	        \    
--disable-multilib                             	        \    
--disable-bootstrap                            		\    
--disable-libgomp
```

**新参数说明:**

* 参数`--enable-languages=c,c++`
> 这个选项确保编译了C 和C++编译器
* 参数`--disable-libstdcxx-pch`
> 不为`libstdc++`编译预编译的头文件(PCH)
> 这会花费很多时间，却对我们没有用处
* 参数`--disable-bootstrap`
> 对于原生编译的 GCC，默认是做一个[引导]构建
> 这不仅会编译GCC一次，而是会编译很多次

---

* 然后执行编译安装等操作
* 在编译并安装过后，可以为其设置符号链接(`gcc->cc`)
> `$ ln -sv gcc /tools/bin/cc`
* 很多程序和脚本执行cc而不是gcc来保证程序的通用性
> 并且在所有的Unix类型的系统上都能用
> 而非仅局限于安装了GCC的Unix 类型的系统

---

### 参考资料

* LFS-v6.2
* LFS-v6.3
* LFS-v9.0

---

