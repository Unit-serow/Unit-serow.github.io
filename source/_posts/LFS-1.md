---
title: LFS-1
date: 2020-02-22 03:55:25
tags: [随笔,GNU/Linux]
categories: [软件,GNU]
---

## Linux from Scratch/LFS-1

---

### 资源整合目录

**Linux from scratch**

* 官方网站[跳转](http://linuxfromscratch.org/)
> http://linuxfromscratch.org/

**LFS LiveCD**

* HTTP获取
> `http://linuxfromscratch.org/livecd/download.html`

* FTP获取
> `http://ftp.osuosl.org/pub/lfs-livecd/lfslivecd-x86-6.3-r2145. iso`

* LFS LiveCD说明[跳转](http://linuxfromscratch.org/livecd/index.html)
> `http://linuxfromscratch.org/livecd/index.html`

* LFS wiki[跳转](https://trac.clfs.org/)
> `https://trac.clfs.org/`

* 操作手册[跳转](http://linuxfromscratch.org/lfs/downloads/9.1-rc1/)
> `http://linuxfromscratch.org/lfs/downloads/9.1-rc1/`

* 中文维基[跳转](https://zh.wikipedia.org/wiki/Linux_From_Scratch)
> `https://zh.wikipedia.org/wiki/Linux_From_Scratch`

* 从LFS官网下载的速度属实不言而喻(无论是FTP还是HTTP)
* 以下链接为永久有效
* Version:`lfslivecd-x86-6.2-3`
* LFS LiveCD 百度网盘地址[跳转](https://pan.baidu.com/s/1IROLau9-OxbN2f-BL3PJVA)
> URL:`https://pan.baidu.com/s/1IROLau9-OxbN2f-BL3PJVA`
> 提取码:y0ss

* Version:`lfslivecd-x86-6.3-r2145`
> 链接[跳转](https://pan.baidu.com/s/1ix83uytHKlvqaOUEa4Rq0w)
> URL:`https://pan.baidu.com/s/1ix83uytHKlvqaOUEa4Rq0w`
> 提取码:dlp4 

* Version:`lfslivecd-x86_64-6.3-r2145`
> 链接[跳转](https://pan.baidu.com/s/1R4T6j07yoR9JAO1U2EoClA)
> URL:`https://pan.baidu.com/s/1R4T6j07yoR9JAO1U2EoClA`
> 提取码:1atk

* linux公社仓库[跳转](https://linux.linuxidc.com/)
> `https://linux.linuxidc.com/`

---

**GNU/Linux LFS Linux From Scratch**

* 基础准备与Linux系统定制原理

* LiveCD
> 利用LFS的方法生成可以自行启动并安装了足够软件的CD
> 可以用来在空机器上安装LFS，或者直接在其上运行应用，已经停止维护

* Linux From Scratch简体中文版(version 9.0)[跳转](https://lctt.github.io/LFS-BOOK/lfs-sysv/LFS-BOOK.pdf)
> `https://lctt.github.io/LFS-BOOK/lfs-sysv/LFS-BOOK.pdf`

* Linux From Scratch简体中文版(全本版)[跳转](https://lctt.github.io/LFS-BOOK/)
> `https://lctt.github.io/LFS-BOOK/`

---

**LFS官方教材所整理的步骤**

* 在宿主操作系统上安装LFS，需要的步骤如下:
* 宿主机即为原主机，原主机可以是GNU/Linux任何发行版

* 对硬盘分区，添加用于安装LFS的用户和组(LFS教科书第2章)
* 下载所有需要的软件包源代码(LFS教科书第3章)
* 准备开发环境(LFS教科书第4章)
* 构造一个基本开发环境(称为工具链/LFS教科书第5章)
* 构造完整的目标系统(LFS教科书第6章)
* 配置系统启动脚本(LFS教科书第7章)
* 启动系统(LFS教科书第8章)
* 相关项目

---

### 补充内容-1

---

* Building and Installing Software Packages for Linux[跳转](http://www.tldp.org/HOWTO/Software-Building-HOWTO.html)
> 软件构建知识Software-Building-HOWTO
> `http://www.tldp.org/HOWTO/Software-Building-HOWTO.html`

* Linux用户手册1[跳转](http://www.linuxfromscratch.org/hints/downloads/files/essential_prereading.txt)
> The Linux Users' Guide
> The Essential Pre-Reading
> `http://www.linuxfromscratch.org/hints/downloads/files/essential_prereading.txt`

* Linux用户手册2[跳转](http://www.linuxhq.com/guides/LUG/guide.html)
> `The Linux Users' Guide 
> http://www.linuxhq.com/guides/LUG/guide.html`

* Linuxsir[跳转](http://www.linuxsir.org/index.html)
> `http://www.linuxsir.org/index.html`

* LFS-内容参考资料
* 作者:孙海勇(冲天飞豹)
* 书籍名称:手把手教你如何建立自己的Linux系统第一版以及第二版
> 2008/2010

* 网络有很多的URL和仓库都已经失效或废除了
* 以我目前拥有的水平与能力，似乎已经找不到更多的参考和资料了
* 即便找到也毫无意义，因为都是搜索引擎已经爬取过的数据了......

---

### FLS-1 补充内容-2

**LFS目录简述与参考:**

* 一阶段
> 第0至1章节-序章与介绍
> 第2至4章节-准备工作
* 二阶段
> 第5章节-临时系统
* 三阶段
> 第6章节-目标系统
* 四阶段
> 第7章节-系统配置
> 第8章节-系统可导
> 第9章节-系统启动(完全抛离)
> 第10章节-最后的清理与附录(尾声)

---

### 相关内容URL整合目录补充内容

* CN-Chroot[跳转](https://zh.wikipedia.org/wiki/Chroot)
> `https://zh.wikipedia.org/wiki/Chroot`

* CN-Linux内核功能[跳转](https://zh.wikipedia.org/wiki/Category:Linux%E5%86%85%E6%A0%B8%E5%8A%9F%E8%83%BD)
> `https://zh.wikipedia.org/wiki/Category:Linux%E5%86%85%E6%A0%B8%E5%8A%9F%E8%83%BD`

* CN-金步国的`Linux-4.4-x86_64`内核配置选项简介[跳转](http://www.jinbuguo.com/kernel/longterm-linux-kernel-options.html)
> `http://www.jinbuguo.com/kernel/longterm-linux-kernel-options.html`

* CN-Unix实用程序列表[跳转](https://zh.wikipedia.org/wiki/Unix%E5%AE%9E%E7%94%A8%E7%A8%8B%E5%BA%8F%E5%88%97%E8%A1%A8)
> `https://zh.wikipedia.org/wiki/Unix%E5%AE%9E%E7%94%A8%E7%A8%8B%E5%BA%8F%E5%88%97%E8%A1%A8`

* EN-Linux From Scratch(Version 9.1-systemd-rc1)[跳转](http://www.linuxfromscratch.org/lfs/downloads/9.1-systemd-rc1/LFS-BOOK-9.1-rc1-NOCHUNKS.html)
> Published February 14th, 2020
> `http://www.linuxfromscratch.org/lfs/downloads/9.1-systemd-rc1/LFS-BOOK-9.1-rc1-NOCHUNKS.html`

---

* EN-Index of /lfs/downloads/9.1-systemd-rc1[跳转](http://www.linuxfromscratch.org/lfs/downloads/9.1-systemd-rc1/)
> `http://www.linuxfromscratch.org/lfs/downloads/9.1-systemd-rc1/`

* EN-Download the Linux From Scratch Book[跳转](http://www.linuxfromscratch.org/lfs/download.html)
> `http://www.linuxfromscratch.org/lfs/download.html`

* CN-LFS(v9.0)[跳转](https://lctt.github.io/LFS-BOOK/lfs-systemd/LFS-SYSD-BOOK.pdf)
> `https://lctt.github.io/LFS-BOOK/lfs-systemd/LFS-SYSD-BOOK.pdf`

* EN-The Linux From Scratch Counter[跳转](http://www.linuxfromscratch.org/cgi-bin/lfscounter.php)
> `http://www.linuxfromscratch.org/cgi-bin/lfscounter.php`

* EN-Linux Sea[跳转](http://swift.siphos.be/linux_sea/)
> `http://swift.siphos.be/linux_sea/`

* EN-其它发行版[Gentoo](http://www.gentoo.org/)[Funtoo](https://www.funtoo.org/Welcome)
> Gentoo: `http://www.gentoo.org/`
> Funtoo: `https://www.funtoo.org/Welcome`

---

### LFS补充内容

* 相关书籍列表

* 《Linux From Scratch》（LFS）
---
* 《Beyond Linux From Scratch》（BLFS）
* 提供了在LFS的基础上，进一步完善Linux基本系统的指引
* 在BLFS中，为系统增加网络、X桌面、声音、打印机和扫描仪支持
> 标准LFS仅仅安装了足够让系统启动的基本软件，以及使新系统能够编译新软件包的开发工具
> BLFS包括了更多的软件包，且都有相应指导
> 从5.0版开始，BLFS开始与LFS的版本号保持同步
---
* 《Cross Linux from Scratch》（CLFS）
* 用于描述交叉编译
* 为需要进行交叉编译(即在一个平台上编译另一个平台的代码)的用户提供指导，正式版本为1.0，另有两个变种
> 《CLFS Sysroot》 采用Sysroot的方法来进行编译，好处是软件包的编译次数可以减少，坏处是不能支持在编译后对软件进行测试，必须要启动到目标平台上才能测试
> 《CLFS Embedded》 一般用于极小系统以及嵌入式系统
> 为此，它使用uclibc而不是一般LFS使用的glibc
> 该项目已停止维护，其官网已无法访问

* 《Hardened Linux From Scratch》（HLFS）
* 此书专注于Linux系统的安全
> 这个子项目致力于打造在安全性上无懈可击的Linux系统
---
* 《Automated Linux From Scratch》（ALFS）
* 标准的LFS只是一本书，用户需要根据书上的指引下载软件包并手动输入指令进行编译
> ALFS子项目提供了把这一切自动化的脚本
---
* Hints
> 收集一些解释性、增强性的文档，以协助用户
---
* LiveCD
> 利用LFS的方法生成可以自行启动并安装了足够软件的CD
> 可以用来在空机器上安装LFS，或者直接在其上运行应用
> 已经停止维护
---
* Patches
> 由于软件之间的依赖关系，在升级软件包之后可能会导致LFS的过程出现故障
> Patch项目致力于研究最新版本的软件之间的互动，并提供一些补丁修复这些故障
---
* 《Community Driven BLFS》(CBLFS)
> 该项目实际是一个Wiki网站
> 依靠网友的自发贡献来提交各种软件包的安装方式

---

### 参考资料:

* CN-中文维基[跳转](https://zh.wikipedia.org/wiki/Linux_From_Scratch)
> `https://zh.wikipedia.org/wiki/Linux_From_Scratch`

* LFS官方网站[跳转](http://www.linuxfromscratch.org/lfs/)
> `http://www.linuxfromscratch.org/`
> `http://www.linuxfromscratch.org/lfs/`

---

### 相关书籍URL补充

---

**ALFS**

* 仓库[跳转](http://www.linuxfromscratch.org/alfs/downloads/jhalfs/stable/)
> `http://www.linuxfromscratch.org/alfs/downloads/jhalfs/stable/`

* 官网[跳转](http://www.linuxfromscratch.org/alfs/download.html)
> `http://www.linuxfromscratch.org/alfs/download.html`

---

**BLFS**

* BLFS-v9.1[跳转](http://www.linuxfromscratch.org/blfs/downloads/stable/BLFS-BOOK-9.1-nochunks.html)
> `http://www.linuxfromscratch.org/blfs/downloads/stable/BLFS-BOOK-9.1-nochunks.html`

* 仓库[跳转](http://www.linuxfromscratch.org/blfs/downloads/)
> `http://www.linuxfromscratch.org/blfs/downloads/`

* 官网[跳转](http://www.linuxfromscratch.org/blfs/download.html)
> `http://www.linuxfromscratch.org/blfs/download.html`

---

**CLFS**

* 官网[跳转](https://trac.clfs.org/)
> `https://trac.clfs.org/`

* 下载界面[跳转](https://trac.clfs.org/wiki/download)
> `https://trac.clfs.org/wiki/download`

**CLFS书籍获取**

* 稳定版
* CLFS 3.0.0 - Systemd
> `$ git clone git://git.clfs.org/cross-lfs.git`
> `$ cd cross-lfs`
> `$ git checkout clfs-3.0.0-systemd`

* 稳定版
* CLFS 3.0.0 - Sysvinit
> `$ git clone git://git.clfs.org/cross-lfs.git`
> `$ cd cross-lfs`
> `$ git checkout clfs-3.0.0-sysvinit`

---

**其它可用参考资源:**

* EN-手册地址[跳转](https://github.com/syl20bnr/spacemacs#linux-distros)
> `https://github.com/syl20bnr/spacemacs#linux-distros`

* CSDN-使用`.emacs.d`目录管理Emacs配置文件[跳转](https://blog.csdn.net/gxp/article/details/6970464)
> `https://blog.csdn.net/gxp/article/details/6970464`

* 某个人博客[跳转](https://bitmingw.com/2017/03/02/spacemacs-install-configuration/)
> `https://bitmingw.com/2017/03/02/spacemacs-install-configuration/`

---



