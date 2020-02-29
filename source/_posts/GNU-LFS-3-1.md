---
title: GNU-LFS-3-1
date: 2020-03-01 00:12:11
tags: [随笔,GNU/Linux]
categories: [软件,GNU]
---

### GNU-LFS-3-1

* 此下任何关于LFS的讨论都是基于LFS-v6.2/6.3的LiveCD与手册之上的
* 程序内所拥有的文件与库这里不做阐述，可参考LFS-v6.2/6.3手册内容

---

**目标主机-1**

* 内核头文件安装
* Glibc安装
* 目标主机工具链解析
* LFS-v6.2/v6.3
* LFS-v6.3-LiveCD

### 内核头文件

**LFS-v6.3**

* [Linux-2.6.22.5]安装流程
> `$ tar xvf $LFS/linux-2.6.22.5.tar.bz2`
> `$ cd linux-2.6.22.5`
> `$ sed -i '/scsi/d' include/Kbuild`
> `$ make mrproper`
> `$ make headers_check` 
> `$ make INSTALL_HDR_PATH=dest headers_install`
> `$ cp -rv dest/include/* /usr/include`
> `$ cd ..`
> `$ rm -rf linux-2.6.22.5`

---

**Linux-Libc-Headers-2.6.12.0**

* 添加一个用户空间头文件和新内核对于`inotify`特性的系统调用支持:
> `$ patch -Np1 -i ../linux-libc-headers-2.6.12.0-inotify-3.patch`

* 安装内核头文件:
> `$ install -dv /usr/include/asm`
> `$ cp -Rv include/asm-i386/* /usr/include/asm` 
> `$ cp -Rv include/linux /usr/include`

* 确保这些头文件的所有者是root:
> `$ chown -Rv root:root /usr/include/{asm,linux}`

* 确保用户可以读取这些头文件:
> `$ find /usr/include/{asm,linux} -type d -exec chmod -v 755 {} \;` 
> `$ find /usr/include/{asm,linux} -type f -exec chmod -v 644 {} \;`

* 此时安装的头文件为`/usr/include/{asm,linux}/*.h`
* 头文件内容可参考LFS-v6.2的6.7.2章节，这里不做过多阐述

---

**Man-pages-2.63/Man-pages-2.34**

* 直接进行编译安装:
> `$ tar xvf $LFS/man-pages-2.63.tar.bz2`
> `$ cd man-pages-2.63`
> `$ make install`
> `$ cd ..`
> `$ rm -rf man-pages-2.63`

---

### Glibc

**Glibc-2.5.1/2.3.6**

* 在进行之前请检查一下是否glibc-2.5.1和glibc-build这两个目录已经被删除，如果没有删除请删除后在继续

* 将glibc-libidn包解压到Glibc的源码目录:
> `$ tar xvf $LFS/glibc-2.5.1.tar.bz2` 
> `$ cd glibc-2.5.1`
> `$ tar -xvf $LFS/glibc-libidn-2.5.1.tar.gz`
> `$ mv glibc-libidn-2.5.1 libidn`

* 应用下面这个patch来修正软件包在`sys/kd.h`之后包含`linux/types.h`导致编译错误:
> `$ patch -Np1 -i ../glibc-2.3.6-linux_types-1.patch`

* 添加一个头文件来定义为新内核对于inotify特性的系统调用函数:
> `$ patch -Np1 -i ../glibc-2.3.6-inotify-1.patch`

* 抑制locale的安装，以避免出现bash的bug
> `$ sed -i '/vi_VN.TCVN/d' localedata/SUPPORTED`

* 当运行make install时，一个叫`test-installation.pl`的脚本会在我们新安装的Glibc上做一个小的完整性测试
* 然而，由于我们的`toolchain`仍然指向`/tools`目录，完整性测试会导致使用错误的Glibc
* 所以必须强制脚本测试刚安装的脚本
```
$ sed -i \ 
's|libs -o|libs -L/usr/lib -Wl,-dynamic-linker=/lib/ld-linux.so.2 -o|' \   
scripts/test-installation.pl 
```

* 继续运行指令:
> `$ sed -i 's|@BASH@|/bin/bash|' elf/ldd.bash.in`
> `$ mkdir -v`
> `$ ../glibc-build`
> `$ cd ../glibc-build`

* 配置安装脚本:
```
$ ../glibc-2.5.1/configure 
--prefix=/usr \ 
--disable-profile \
--enable-add-ons \ 
--enable-kernel=2.6.0 \
--libexecdir=/usr/lib/glibc
```

* 新参数说明:
* 参数`--libexecdir=/usr/lib/glibc`
> 把`pt_chown`程序的位置从默认的`/usr/libexec`改为`/usr/lib/glibc`

> `$ make`

* 对结果进行测试:
> `$ make -k check 2>&1 | tee glibc-check-log`
> `$ grep Error glibc-check-log`

* 在安装Glibc的过程中，它会警告缺少`/etc/ld.so.conf`文件
* 其实这没什么关系，不过下面的命令能修正它:
> `$ touch /etc/ld.so.conf`

> `$ make install`

* (LFS-v6.2独有)此部还需要安装`inotify头文件`到系统头文件的地方:
> `$ cp -v ../glibc-2.3.6/sysdeps/unix/sysv/linux/inotify.h \ /usr/include/sys`

* 一次安装所有列在`glibc-2.3.6/localedata/SUPPORTED`中的`locales`
> `$ make localedata/install-locales`
---
**配置Glibc**

* 此时需要建立`/etc/nsswitch.conf`文件
* 因为在这个文件丢失或不正确的情况下，Glibc会使用默认配置，而Glibc的默认配置无法很好地在网络环境下工作
* 并且我们也需要设置自己的时区
* 建立一个新的`/etc/nsswitch.conf`文件:
```
$ cat > /etc/nsswitch.conf << "EOF" 
# Begin /etc/nsswitch.conf 
passwd: files 
group: files 
shadow: files
hosts: files dns 
networks: files 
protocols: files 
services: files 
ethers: files 
rpc: files 
# End /etc/nsswitch.conf 
EOF 
```

* 设置时区:
> `$ cp -v --remove-destination /usr/share/zoneinfo/Asia/Shanghai /etc/localtime`

* 配置动态链接库加载程序
* 写入配置
* LFS-v6.3
````
$ cat > /etc/ld.so.conf << "EOF" 
/usr/local/lib 
/opt/lib 
EOF
```
* LFS-v6.2
```
$ cat > /etc/ld.so.conf << "EOF"
# Begin /etc/ld.so.conf
/usr/local/lib 
/opt/lib
# End /etc/ld.so.conf 
EOF
```

> `$ cd ..`
> `$ rm -rf glibc-build`
> `$ rm -rf glibc-2.5.1`

* glibc的测试比较容易出现错误，比如机器慢就有可能出现超时的错误，还有一些能引起错误的LFS手册上有所提及
* 由此某些情况的错误可以无视

---


### 调整目标主机工具链

* 现在，最终的C库已经安装好了，此时需要再次调整工具链，让本章随后编译的那些工具都连接到这个库上
* 基本上，就是把临系统时增加中调整工具链那里做的调整给取消掉
* 在临时系统中，工具链使用的库是从宿主系统的`/{,usr/}lib`转向新安装的`/tools/lib`目录
* 同样的，现在工具链使用的库将从临时的`/tools/lib`转向LFS系统最终的`/{,usr/}lib`目录 

* 首先，备份`/tools`下的链接
> 用刚才在临时主机中编译的链接器来替换
> 再创建一个链接到在`/tools/$(gcc -dumpmachine)/bin`中的副本
* 执行以下命令:
> `$ mv -v /tools/bin/{ld,ld-old}`
> `$ mv -v /tools/$(gcc -dumpmachine)/bin/{ld,ld-old}`
> `$ mv -v /tools/bin/{ld-new,ld}`
> `$ ln -sv /tools/bin/ld /tools/$(gcc -dumpmachine)/bin/ld`

* 接下来，修正GCC的specs文件，使它指向新的动态链接器
* 这样GCC才能知道在哪能发 现开始文件
* 这里应用一个sed命令:
```
$ gcc -dumpspecs | sed \ 
-e 's@/tools/lib/ld-linux.so.2@/lib/ld-linux.so.2@g' \ 
-e '/\*startfile_prefix_spec:/{n;s@.*@/usr/lib/ @}' \ 
-e '/\*cpp:/{n;s@$@ -isystem /usr/include@}' > \ 
`dirname $(gcc --print-libgcc-file-name)`/specs
```
* 还可以利用perl命令
```
$ gcc -dumpspecs | \ 
perl -p -e	's@/tools/lib/ld-linux.so.2@/lib/ld-linux.so.2@g;' \
-e 's@\*startfile_prefix_spec:\n@$_/usr/lib/ @g;' > \
`dirname	$(gcc --print-libgcc-file-name)`/specs
```

* 如果此时本地主机的系统平台上的动态连接器的名字不是`ld-linux.so.2`
* 必须把上面命令里的`ldlinux.so.2`换成此时本地主机的系统平台上动态连接器的名字

---


