---
title: GNU GRUB
date: 2020-02-28 01:04:40
tags: [GNU/Linux,随笔]
categories: [软件,Disk]
---

### GRUB 简述

* 概述
* 启动过程(逻辑)
* 特性(相对于LILO或其它的引导程序)
* 相关概念

**概述:**

* GNU GRUB，简称GRUB
* 基于GNU通用公共许可证
* 是一个来自GNU项目的启动引导程序
* GRUB是多启动规范的实现，它允许用户可以在计算机内同时拥有多个操作系统并在计算机启动时选择希望运行的操作系统
* GRUB可用于选择操作系统分区上的不同内核，也可用于向这些内核传递启动参数
* GNU GRUB的前身为Grand Unified Bootloader
* 它主要用于类Unix系统
* 同大多Linux发行版一样，GNU系统也采用GNU GRUB作为它的启动器
* Solaris从10 1/06版开始在x86系统上也采用GNU GRUB作为启动器

---

**GRUB启动过程:**
1. 计算机启动后，BIOS将寻找第一个可启动的设备(通常为硬盘)
2. 而后从MBR中加载启动程序，然后把控制交给这段代码
3. MBR位于硬盘的前512字节内

* GRUB第一版的启动过程
1. GRUB的步骤1包含在MBR中
> 由于受MBR的大小限制，步骤1所做的几乎只是装载GRUB的下一步骤(存放在硬盘的其它位置)
2. 步骤1既可以直接装载步骤2，也可以装载步骤1.5: GRUB的步骤1.5包含在MBR后面的30千字节中
3. 步骤1.5加载步骤2
4. 当步骤2启动后，它将呈现一个界面来让用户选择启动的操作系统
> 这步通常采用的是图形菜单的形式，如果图形方式不可用或者用户需要更高级的控制
> 可以使用GRUB的命令行提示，通过它，用户可以手工指定启动参数
> GRUB还可以设置超时后自动从某一个内核启动

* GRUB第二版的启动过程
* 与GRUB第一版相似的是，`boot.img`像步骤1一样在MBR或在启动分区中
> 但是，它可以从任何LBA48地址的一个扇区中读取
1. 它(boot.img)将读取core.img(产生于diskboot.img)的第一个扇区以用来后面读取core.img的剩余部分
2. core.img正常情况下跟步骤1.5储存在同一地方并且有着同样的问题
> 可是，当他被移动到一个文件系统或一个纯粹的分区时会比在步骤1.5移动或删除引起更少的麻烦
> 一旦完成读取，core.img会读取默认的配置文件和其他需要的模块

* 当GRUB启动后的执行逻辑(NT内核的特点)
* 一旦选择了启动选项，GRUB把选择的内核加载内存并把控制交给内核
> 在此步骤中，对于Windows之类不支持多启动标准的操作系统，GRUB也可以通过链式启动把控制传给其它启动器
> 在这种情况下，其它操作系统的启动程序被GRUB保存了下来
* 与内核不同，其它操作系统如同直接自MBR启动
> 类似Windows的启动菜单，也许是另一个启动管理器，它允许在多个不支持多启动的操作系统中做进一步的选择
> 在已有Windows的系统上面，或者包含多个Windows版本的系统上安装现代的Linux而不修改原操作系统，即属于这类情况

---

**GRUB特点:**

* GRUB的一个重要的特性是安装它不需依附一个操作系统
> 但是，这种安装需要一个Linux/Windows副本
> 由于单独工作，GRUB实质上是一个微型系统，通过链式启动的方式，它可以启动所有安装的主流操作系统
* 与LILO不同，修改GRUB的配置文件后，不必把GRUB重新安装到MBR或者某个分区中

* 在Linux中，`$grub-install`命令是用来把GRUB的步骤1安装到MBR或者分区中的
> GRUB的配置文件、步骤2以及其它文件必须安装到某个可用的分区中
> 如果这些文件或者分区不可用，步骤1将把用户留在命令行界面

* GRUB Legacy的配置文件
> 为`/boot/grub/menu.lst`或`/boot/grub/grub.conf`
* GRUB 2的配置文件
> 为`/boot/grub/grub.conf`

* 除了硬盘外，GRUB也可安装到光盘、软盘和闪存盘等移动介质中
> 以此引导一台无法从硬盘启动的系统

---

**相关概念(关键字):**
* LILO
* SYSLINUX
* GRUB
* UEFI
* BIOS
* MBR
* GPT
* NTLDR
* Windows Boot Manager

---

### GRUB 使用方法与相关指令简述

* grub命令是多重引导程序grub的命令行shell工具
* 基本语法:
> `$grub [options]`
* 直接键入grub则直接进入grub命令行
* 其它参数这里不过过多阐述
---
* 正常启动情况下，屏幕上出现grub的启动项选择菜单时按`c键`也是可以进入`grub>`状态的
* grub指令最重要且最常用的功能就是用来启动损坏的或者是LFS的已独立系统
* 用grub的命令来手工启动系统只需要用到四个命令`boot`，`kernel`，`initrd`，`boot`
* 参数`--help`用于显示帮助信息

* 列出当前电脑上可能的磁盘设备
> `grub> root (hd/sd`
> 然后按两次TAB键
> 通常会输出硬盘为`hd0/hd1`或`sd0/sd1`等

* 选择本地主机的安装Linux系统的硬盘
* 比如`hd0`，执行
> `grub> root (hd0,`
> 再按两次TAB键
> 通常输出并列出本地主机第一块硬盘上的分区情况
> 此时可以知道哪个是swap交换分区(0x82)或哪个是Linux分区(0x83)
* 然后选择可能的/boot目录所在的分区
> 执行`root (hd0, 1)`并回车

* 查看所选分区是否为`/boot`所在分区(根目录分区判断)
> `grub> cat /xxx/xxx`
> xxx为指定文件目录
> 按两次TAB键
* 这里以输入`cat /sbin/init`来举例，连按两次TAB键之后参考以下两种情况:
1. 如果出现一些init开头的文件，则说明该分区为`/`所在的分区
2. 如果没有出现/sbin/init文件，说明(hd0,1)分区仅仅是`/boot`分区而不是`/`分区
> 此时需要重新输入`$root (hd0,N)`命令，这里N是某个Linux分区
> 然后再试`cat /sbin/init`， 直到屏幕上出现`/sbin/init`
> 则说明找到了`/`分区
> 严格来说，应该是`/sbin`目录所在的分区
* 此指令还可用于判断所选分区内的文件目录与拥有文件，利用所存储文件的类别来判断分区的作用及分区名
* 这里的关键问题是如何确定系统的几个分区: `/boot`，`/`与`/sbin`

* 比如输入`cat /boot/vm`并按两次TAB键
> 如果出现一些`vm`开头的文件，比如`vmlinuz-2.6.15-26-386`说明这里是`/boot`所在的分区
* 再输入`cat /boot/initrd`并按两次TAB键
> 如果出现一些`initrd`开头的文件，比如`initrd.img-2.6.15-26-386`说明这个`/boot`所在的分区有`initrd`即`ramdisk`镜像

**通用指令集:**

* 一般情况下，依次输入以下命令即可以进入(启动)系统
> `root (hd0,1)`   # 此时假设`/dev/hda2`是本地主机的`/boot`所在的分区
> `kernel /boot/vmlinuz-2.6.15-26-386 ro dev=/dev/hda3`   # 此时假设`/dev/hda3`是本地主机的根目录`/`所在的分区
> `initrd /boot/initrd.img-2.6.15-26-386`
> `boot`
双引号
---

### 参考资料

* CN-WIKI-GNU GRUB[跳转](https://zh.wikipedia.org/wiki/GNU_GRUB)
> `https://zh.wikipedia.org/wiki/GNU_GRUB`

* EN-GNU 官网[跳转](https://www.gnu.org/software/grub/)
> `https://www.gnu.org/software/grub/`

* EN-GNU 手册[跳转](https://www.gnu.org/software/grub/manual/grub/)
> `https://www.gnu.org/software/grub/manual/grub/`

* CN-GRUB 2 中文指南[跳转](http://wiki.ubuntu-tw.org/index.php?title=GRUB_2_%E4%B8%AD%E6%96%87%E6%8C%87%E5%8D%97)
> `http://wiki.ubuntu-tw.org/index.php?title=GRUB_2_%E4%B8%AD%E6%96%87%E6%8C%87%E5%8D%97`

* CN-GRUB入门教程(Ubantu论坛)[跳转](https://forum.ubuntu.org.cn/viewtopic.php?t=2475)
> `https://forum.ubuntu.org.cn/viewtopic.php?t=2475`

* EN-mmap.page[跳转](https://mmap.page/)
> `https://mmap.page/`

* CN-GRUB指令集整合[跳转](https://man.linuxde.net/grub)
> `https://man.linuxde.net/grub`

* CN-Linux命令大全[跳转](https://man.linuxde.net/)
> `https://man.linuxde.net/`

---



