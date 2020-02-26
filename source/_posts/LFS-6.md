---
title: LFS-6
date: 2020-02-26 20:38:21
tags: [随笔,GNU/Linux]
categories: [软件,GNU]
---

## LFS-6

---

### LFS实现逻辑补充


**LFS的实现大致可分为以下四个阶段:**
* 一阶段
1.创建目标系统目录
2.创建临时系统目录
* 二阶段
3.建立预工具链
* 三阶段
4.建立临时系统
5.建立目标工具链
* 四阶段
6.建立目标系统
7.收尾工作

---

## 临时系统

3. **建立预工具链**
* 预工具链
* 汇编器Binutils，编译器GCC，标准库Glibc
* 以及主系统(内核头接口/API headers)
> API headers/GCC/BIN/GLI

* 调整工具链
> 每次安装完工具链想用工具集时都需要适当的调整工具链并对工具链进行测试
* Glibc编译过程中需要设置内核版本参数(可忽略小版本只写大版本)

* 二次安装工具目录(GCC/Bintils)
* Tcl-v8.4 
* Expect-v5.4
* DejaGNU-v1.4
* GCC-Pass2
* Binutils-Pass2
* 其它辅助程序(工具)
* Tcl/Expect/DejaGNU为代码(二进制)编译文件测试工具
> `$make check`

---

### 预工具链安装逻辑:

1. Binutils-2.17 - Pass 1
2. GCC-4.1.2 - Pass 1
3. Linux-2.6.22.5 API Headers
3. Glibc-2.5.1
4. Adjusting the Toolchain(调整工具链)
5. Tcl-8.4.15
6. Expect-5.43.0
7. DejaGNU-1.4.4
8. GCC-4.1.2 - Pass 2
9. Binutils-2.17 - Pass 2
10. 其它辅助工具

---

**所对应LFS内章节内容:**

5. Constructing a Temporary System(建立一个临时系统)
* Introduction (介绍与说明)
* Toolchain Technical Notes (工具链技术说明)
* Binutils-2.17 - Pass 1 (汇编器)
* GCC-4.1.2 - Pass 1 (编译器)
* Linux-2.6.22.5 API Headers (内核接口)
* Glibc-2.5.1 (标准库)
* 至
* Util-linux-2.12r (UTIL)
* Stripping (抛离)
* Changing Ownership (改变所有权)
* 临时系统建立至此截止

---

## 目标系统

**第一步(进行必要配置):**

1. 建立目标系统的文件目录结构
2. 创建与配置必要软链接
3. 创建root及nobody用户和必要的组
4. 此时可以选择是否重新加载bash
5. 加载以使root用户起效
6. 创建和设置几个临时文件和日志文件

**第二步(建立目标工具链):**

* 包括安装逻辑说明
* Linux-2.6.22.5 API Headers - 1
* Man-pages-2.63 - 2
* Glibc-2.5.1 - 3
* Re-adjusting the Toolchain(工具链调试) - 4
* Binutils-2.17 - 5
* GCC-4.1.2 - 6
* 其它辅助工具 (Shell/Bash，M4，Autotools等等) - 7
* 至此，一直到所有软件安装完毕后，进行工具链调试(v6.3的FSL中最后一个工具通常是vim)
* 之后退出chroot环境，设置启动脚本
* 下一步即为第七章-设置系统启动脚本然后进行最终的内核编译(Kernel Compile)

---

### 建立目标工具链以及目标工具链环境:

**参考章节**

**三.建立LFS系统(III.Building the LFS System)**

6. Installing Basic System Software (6.安装基本系统软件)
* Introduction (介绍)
* Preparing Virtual Kernel File Systems (准备虚拟内核文件系统)
* Package Management (包装管理)
* Entering the Chroot Environment (进入Chroot环境)
* Creating Directories (创建目录)
* Creating Essential Files and Symlinks (创建基本文件和符号链接)
* Linux-2.6.22.5 API Headers (Linux-2.6.22.5 API标头)
* Man-pages-2.63 (Man-帮助手册)
* Glibc-2.5.1 (标准库)
* Re-adjusting the Toolchain (重新调整工具链)
* Binutils-2.17 (汇编器)
* GCC-4.1.2 (编译器)
* 至
* About Debugging Symbols (调试符相关内容)
* Stripping Again (再次抛离)
* Cleaning Up (清理环境)
* 目标系统环境已搭建完毕

---

### 系统启动脚本设置与编译(包括编写)
**参考自LFS英文版第七章内容:**
**7. Setting Up System Bootscripts**

* 介绍 (Introduction)
* LFS-Bootscripts-6.3 (LFS-boot 脚本)
* 至
* 创建到设备的自定义符号链接 (Creating Custom Symlinks to Devices)
* 配置网络脚本 (Configuring the network Script)

**配置逻辑说明:**

1. 编译并安装 LFS-Bootscripts-6.3 (LFS-Bootscripts-6.3)
2. 配置LFS系统上的设备和模块处理 (Device and Module Handling on an LFS System)
3. 配置setclock脚本 (Configuring the setclock Script)
4. 配置Linux控制台  (Configuring the Linux Console)
5. 配置sysklogd脚本 (Configuring the sysklogd Script)
6. 创建/etc/inputrc文件 (Creating the /etc/inputrc File)
7. Bash Shell启动文件 (The Bash Shell Startup Files)
8. 配置本地网脚本 (Configuring the localnet Script)
9. 定制/etc/hosts文件 (Customizing the /etc/hosts File)
10. 创建到设备的自定义符号链接 (Creating Custom Symlinks to Devices)
11. 配置网络脚本 (Configuring the network Script)
* 至此结束系统启动脚本配置，下一步即为内核编译

---

### 配置LFS系统引导项(内核编译)
**参考自FLS文档第八章**
**8. Making the LFS System Bootable**

**配置逻辑介绍(参考内容):**

1. 介绍 (Introduction)
2. 创建/etc /fstab文件 (Creating the /etc/fstab File)
3. Linux-2.6.22.5 (Linux-2.6.22.5编译，配置并安装)
4. 使LFS系统可启动 (Making the LFS System Bootable)

* 相关指令集可参考官方文档
* 有关第三项的详细说明与配置参考下一篇文章

---

**其它内容:**

* 具体配置内容与描述可参考官方文档(EN/CN)
* 这里使用的是LFS官方的LiveCD，官方早已停止维护，所以版本已经很老了
* 最新的版本是`lfslivecd-x86_64-6.3-r2145.iso`(614.510KB)-2007
* 这里使用的版本是`lfslivecd-x86-6.3-r2145.iso`(32位版本/648.638KB)-2007
* 在[LFS-1](http://unit-serow.com/2020/02/22/LFS-1/#more)这篇文章内有有关LFS所有资料的链接
> `http://unit-serow.com/2020/02/22/LFS-1/#more`
---
* 对于目标系统中的任何工具的编译完成之后，最好进行编译文件(二进制文件)测试是否正确且可用
* 即便有错误，只要不是太多或可以通过下一步的应用测试，就可以先无视掉
* 等到目标系统内核建立并编译完成之后再对目标Debug进行修补与维护
* 测试指令(测试动态链接库): `$make check`
* 测试时间长短由工具决定
* 有些二进制包在测试时可能会发生几处无关紧要的错误，但不会影响安装和正常使用
> 比如类似于找不到man的动态链接库之类的错误
* 有时测试不能顺利结束，可以根据报错来判断问题所在
> 多半是文件依赖，动态库，文件映射或配置文件缺失等问题

---

### 需调整工具链:

* 工具链一(预/临时工具链):
> 预工具链与临时工具链(GCC/Glibc/Binutils/Linux Kernel API Headers)
> 调整specs文件
> 调试与测试所属工具链环境

* 工具链二(目标工具链):
> 目标工具链(GCC/Glibc/Linux Kernel API Headers/Binutils/Man-pages)
> 调整specs文件
> 调试与测试所属工具链环境

* 最后执行Strip命令并进入新的chroot环境

* 即为拥有两次抛离过程
> 第一次是主系统-临时系统
> 第二次是临时系统-目标系统
> 最后保证目标系统可以独立运行并将其独立(完全抛离原系统)

---

### 参考文献

* 具体的配置代码与安装代码可参考LFS官方中/英文书籍
* CN-参考资料FSL为6.3版本[跳转](http://www.linuxfromscratch.org/lfs/view/6.3/index.html)
> `http://www.linuxfromscratch.org/lfs/view/6.3/index.html`

---
