---
title: LFS-5
date: 2020-02-26 04:21:50
tags: [随笔.GNU/Linux]
categories: [软件,GNU]
---

## LFS-5

* 应用笔记以及经验总结

---

### 首要逻辑说明:

* 编译工具就是汇编工具与语言编译器(Binutils/GCC)
* 汇编工具，语言编译器，对应语言标准库被合称为工具链(Binutils/GCC/Glibc)
> 工具链的配置即为以上三个工具的配置
> 因为让编译工具生成可执行文件需要对应标准库，所以这里将标准库算到工具链内(严格来说标准库并不是工具)
* 辅助命令
* 文件(目录)映射

---

1. 创建目标系统目录
2. 创建临时系统目录
3. 建立预工具链
4. 建立临时系统
5. 建立目标工具链
6. 建立目标系统
7. 收尾工作

---

**作用解释:**
* `CC="gcc -B/usr/bin"`
* 在第一遍编译GCC中是调用/tools内的gcc
> 调用GCC作为编译器，指定GCC运行环境为/usr/bin
*  在第一遍编译Binutils时是调用/tools内的GCC，接下来指定链接器指向
* 在第二遍编译Binutils中是在调用host中的GCC

---

**注意事项(相关内容):**
* 设置工具链的时候必须保证工具处于可用状态
* 有些程序和工具可能需要编译及安装两遍以上
* 在目标机器内Glibc的测试比较容易出现错误，比如机器慢就有可能出现超时的错误
> 还有一些能引起错误的LFS手册上有所提及
> 类似于超时这种 错误有时候很难避免
> 只能跳过去或进行多次编译以及安装
* 跳过对于目标机器内Glibc及其工具链的测试
* 有一两个Error就忽略吧
* 测试代码并统计
> `$make check`
> 测试统计有可能会出现个别失败
> 有时会完全成功
* 参考资料均来自十年前(最少)
* 参考资料本身没什么太大问题

---

### 问题一览

* 待解决问题
> v6.2 无内核头部配置文件
> v6.3 第二次编译C函数库(Glibc)时出错
> v6.3 目标工具链-Binutils编译出现错误，没有通过测试，并且已无视
> v6.3 目标工具链-GCC编译出现几处错误，但不影响使用并已成功通过安装测试与应用测试
> v6.3 测试Automake-1.10工具源代码编译文件时出现三个错误，但无伤大雅
> v6.3 Linux内核编译出现问题(kernel version:2.6.22.5)
> v6.3 找不到GCC
---
* 目标机器内的Glibc标准函数库测试错误问题已解决
* 目标机器内的GCC编译器问题已解决
* 目标工具链内的GCC安装与应用测试成功
* 编译Coreutils-6.9出现两处Error
> 动态链接库测试中编译帮助文件`man目录`失效
> `BEGIN failed--compilation aborted at ./help2man line 28`
> 离开`*/man`目录
> 已经无视，并且进行代码测试后也是这个问题
* Procps-3.2.7(Top)
> `collect2: ld returned 1 exit status`
> make停止
> 安装失败
* Perl-5.8.8
> 动态链接库测试中编译出现两条错误
> 并不妨碍正常编译安装，并且编译安装成功
* Readline-5.2
> 动态链接库测试中编译出现一条错误
> 并不妨碍正常编译安装，并且编译安装成功
* Automake-1.10
> 动态链接库测试中编译出现三条错误
> 并不妨碍正常编译安装，并且编译安装成功
* Psmisc-22.5
> cannot find tinfo，ncurses or termcap libraries
> 无法找到无法找到tinfo、ncurses或termcap库
> 编译失败
* Udev-113
> make test测试与安装无错误
* 到达第七章与第八章之间的退出chroot出现问题
> 根据LFS官方手册配置，进入新的系统环境下GCC丢失
> 未解决

---

### 参考资料

* 开源中国[跳转](https://www.oschina.net/)
> `https://www.oschina.net/`

---

* LFS注册[跳转](http://www.linuxfromscratch.org/cgi-bin/lfscounter.php)
> `http://www.linuxfromscratch.org/cgi-bin/lfscounter.php`

---

* LFS-6.3版本[跳转](http://www.linuxfromscratch.org/lfs/view/6.3/)
> `http://www.linuxfromscratch.org/lfs/view/6.3/`
---

* LFS-6.3内核编译(kernel version:2.6.22.5)[跳转](http://www.linuxfromscratch.org/lfs/view/6.3/chapter08/kernel.html)
> `http://www.linuxfromscratch.org/lfs/view/6.3/chapter08/kernel.html`

---

* 冲天飞豹Blog(已经挂了)
> `http://youbest.cublog.cn/`

---

* LFS-PDF[跳转](https://pan.baidu.com/s/1nZARmQlO63fh5BVGug4gPg)
> 链接:`https://pan.baidu.com/s/1nZARmQlO63fh5BVGug4gPg`
> 提取码:414z

---

### 重要工具与程序简述(小部分/最新版本):

* Glibc (2.30) - 16,189 KB:
> 主页: `http://www.gnu.org/software/libc/`
> 下载: `http://ftp.gnu.org/gnu/glibc/glibc-2.30.tar.xz`
> MD5 校验和: `2b1dbdf27b28620752956c061d62f60c`

* GCC (9.2.0) - 68,953 KB:
> 主页: `https://gcc.gnu.org/`
> 下载: `http://ftp.gnu.org/gnu/gcc/gcc-9.2.0/gcc-9.2.0.tar.xz`
> MD5 校验和: `3818ad8600447f05349098232c2ddc78`

* Linux (5.2.8) - 104,555 KB:
> 主页: `https://www.kernel.org/`
> 下载: `https://www.kernel.org/pub/linux/kernel/v5.x/linux-5.2.8.tar.xz`
> MD5 校验和: `602dd0ecb8646e539fefb2beb6eb6fe0`

* Binutils (2.32) - 20,288 KB:
> 主页: `http://www.gnu.org/software/binutils/`
> 下载: `http://ftp.gnu.org/gnu/binutils/binutils-2.32.tar.xz`
> MD5 校验和: `0d174cdaf85721c5723bf52355be41e6`

* GRUB (2.04) - 6,245 KB:
> 主页: `http://www.gnu.org/software/grub/`
> 下载: `https://ftp.gnu.org/gnu/grub/grub-2.04.tar.xz`
> MD5 校验和: `5aaca6713b47ca2456d8324a58755ac7`

* LFS-Bootscripts (20190524) - 32 KB:
> 下载: `http://www.linuxfromscratch.org/lfs/downloads/9.0/lfs-bootscripts-20190524.tar.xz`
> MD5 校验和: `c91b11e366649c9cec60c2552820fed5`

---

* Autoconf (2.69) - 1,186 KB:
> 主页： http://www.gnu.org/software/autoconf/
> 下载： http://ftp.gnu.org/gnu/autoconf/autoconf-2.69.tar.xz
> MD5 校验和： 50f97f4159805e374639a73e2636f22e

* Automake (1.16.1) - 1,499 KB:
> 主页： http://www.gnu.org/software/automake/
> 下载： http://ftp.gnu.org/gnu/automake/automake-1.16.1.tar.xz
> MD5 校验和： 53f38e7591fa57c3d2cee682be668e5b

* Bash (5.0) - 9,898 KB:
> 主页： http://www.gnu.org/software/bash/
> 下载： http://ftp.gnu.org/gnu/bash/bash-5.0.tar.gz
> MD5 校验和： 2b44b47b905be16f45709648f671820b

* File (5.37) - 867 KB:
> 主页： https://www.darwinsys.com/file/
> 下载： ftp://ftp.astron.com/pub/file/file-5.37.tar.gz
> MD5 校验和： 80c29aca745466c6c24d11f059329075

* Libtool (2.4.6) - 951 KB:
> 主页： http://www.gnu.org/software/libtool/
> 下载： http://ftp.gnu.org/gnu/libtool/libtool-2.4.6.tar.xz
> MD5 校验和： 1bfb9b923f2c1339b4d2ce1807064aa5

* M4 (1.4.18) - 1,180 KB:
> 主页： http://www.gnu.org/software/m4/
> 下载： http://ftp.gnu.org/gnu/m4/m4-1.4.18.tar.xz
> MD5 校验和： 730bb15d96fffe47e148d1e09235af82

* Make (4.2.1) - 1,932 KB:
> 主页： http://www.gnu.org/software/make/
> 下载： http://ftp.gnu.org/gnu/make/make-4.2.1.tar.gz
> MD5 校验和： 7d0dcb6c474b258aab4d54098f2cf5a7

* OpenSSL (1.1.1c) - 8,657 KB:
>主页： https://www.openssl.org/
> 下载： https://www.openssl.org/source/openssl-1.1.1c.tar.gz
> MD5 校验和： 15e21da6efe8aa0e0768ffd8cd37a5f6

---

* Gawk (5.0.1) - 3,063 KB:
> 主页： http://www.gnu.org/software/gawk/
> 下载： http://ftp.gnu.org/gnu/gawk/gawk-5.0.1.tar.xz
> MD5 校验和： f9db3f6715207c6f13719713abc9c707

* Util-linux (2.34) - 4,859 KB:
> 主页： http://freecode.com/projects/util-linux
> 下载： https://www.kernel.org/pub/linux/utils/util-linux/v2.34/util-linux-2.34.tar.xz
> MD5 校验和： a78cbeaed9c39094b96a48ba8f891d50

* Zlib (1.2.11) - 457 KB:
>主页： https://www.zlib.net/
>下载： https://zlib.net/zlib-1.2.11.tar.xz
> MD5 校验和： 85adef240c5f370b308da8c938951a68

---

**补丁:**

* Coreutils 国际化修复补丁 - 168 KB:
> 下载： http://www.linuxfromscratch.org/patches/lfs/9.0/coreutils-8.31-i18n-1.patch
> MD5 校验和： a9404fb575dfd5514f3c8f4120f9ca7d

* Glibc FHS 补丁 - 2.8 KB:
> 下载： http://www.linuxfromscratch.org/patches/lfs/9.0/glibc-2.30-fhs-1.patch
> MD5 校验和： 9a5997c3452909b1769918c759eff8a2

---

### 已解决问题一览

* 如果实在找不到GCC且有难以解决的问题，可以先利用已有的临时主机中的/tools目录来对目标主机进行错误与空白修补
* 各参数作用这里不做过多赘述，可参考LFS官方手册

---

* 参考自LFS-v6.3版本第6.4-Entering the Chroot Environment至6.59-Stripping Again章节
* 第七章末尾找不到GCC的问题已解决
> 需要先完全配置才能去抛离上一级系统目录环境(此时需要脱离的是临时系统)
> 在第六章开头理解出问题了
> 在查询了FSL官方的英文文档之后
> 发现退出chroot的代码只需要执行一遍
> chroot及附带配置的作用是抛离前(是属于目标系统的)的配置
> 使用Strip对文件(二进制压缩包)进行清理

**可参考以下指令:**

1. 退出chroot环境:
> `$logout`

2. 为Strip而进入chroot环境:
```
chroot $LFS /tools/bin/env -i \
    HOME=/root TERM=$TERM PS1='\u:\w\$ ' \
    PATH=/bin:/usr/bin:/sbin:/usr/sbin \
    /tools/bin/bash --login
```

3. Strip:
```
/tools/bin/find /{,usr/}{bin,lib,sbin} -type f \
  -exec /tools/bin/strip --strip-debug '{}' ';'
```

---

* 摘选自LFS-v6.3/EN-CN(翻译)
> A large number of files will be reported as having their file format not recognized.
> These warnings can be safely ignored.
> These warnings indicate that those files are scripts instead of binaries.
* 翻译内容:
> 大量文件将被报告为文件格式无法识别
> 可以安全地忽略这些警告
> 这些警告表明这些文件是脚本而不是二进制文件

---

**补充内容:**

* 摘选自FSL官方文档:
> From now on, when reentering the chroot environment after exiting, use the following modified chroot command:
```
chroot "$LFS" /usr/bin/env -i \
    HOME=/root TERM="$TERM" PS1='\u:\w\$ ' \
    PATH=/bin:/usr/bin:/sbin:/usr/sbin \
    /bin/bash --login
```
> The reason for this is that the programs in /tools are no longer needed. Since they are no longer needed you can delete the /tools directory if so desired.

* 翻译内容:
> 从现在开始，退出后重新进入chroot环境时，请使用以下修改后的chroot命令：
> 这样做的原因是/tools不再需要其中的程序
> 因为不再需要它们，所以可以根据需要来决定是否去删除/tools目录

---

**补充内容:**

* 6.4章节中描述的带有临时机器中的/tools文件夹的目标机器
> It is time to enter the chroot environment to begin building and installing the final LFS system. As user root, run the following command to enter the realm that is, at the moment, populated with only the temporary tools:
* 翻译内容:
> 现在是时候进入chroot环境开始构建和安装最终的LFS系统了
> 以user root身份，运行以下命令以输入当前仅由临时工具填充的领域:
```
chroot "$LFS" /tools/bin/env -i \
    HOME=/root TERM="$TERM" PS1='\u:\w\$ ' \
    PATH=/bin:/usr/bin:/sbin:/usr/sbin:/tools/bin \
    /tools/bin/bash --login +h
```

---

**重点内容-1**
* 6.2.章节 准备虚拟内核文件系统
* 6.22章节 挂载和激活/dev

---

**参考资料:**

* 6.4 Entering the Chroot Environment[跳转](http://www.linuxfromscratch.org/lfs/view/6.3/chapter06/chroot.html)
> `http://www.linuxfromscratch.org/lfs/view/6.3/chapter06/chroot.html`

* 6.59. Stripping Again[跳转](http://www.linuxfromscratch.org/lfs/view/6.3/chapter06/strippingagain.html)
> `http://www.linuxfromscratch.org/lfs/view/6.3/chapter06/strippingagain.html`

* 6.60. Cleaning Up[跳转](http://www.linuxfromscratch.org/lfs/view/6.3/chapter06/revisedchroot.html)
> `http://www.linuxfromscratch.org/lfs/view/6.3/chapter06/revisedchroot.html`

---

---
