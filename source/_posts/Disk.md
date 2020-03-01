---
title: Disk-1
date: 2020-02-28 11:08:36
tags: [随笔]
categories: [软件,Disk]
---

## Disk-1

---

### Disk 引导逻辑全过程描述

* 磁盘从底层固件引导至操作系统启动所对应的执行逻辑
* 本篇内容仅为主观描述，仅供参考

**执行逻辑简述:**

Linux
> `BIOS/UEFI(ROM)->MBR/GPT/GUID-(LBA/CHS)->VBR->grldr->boot loader->GRUB/LILO...->启动整个Linux系统`

windows
> `BIOS->MBR->DPT->PBR->Bootmgr->BCD->系统选择界面-->选择windows-NT->Winload.exe->内核加载等 ->启动整个windows-NT系统`

**文字描述:**
* 1. 先给基于ROM的固件BIOS/UEFI通电(启动/运行)，以加载磁盘主引导程序
* 2. POST(Power-On Self-Test)，基于BIOS程序进行对本地主机的硬件自检
* 3. 基于对应固件类别来加载引导扇区(Boot Sequence)
> BIOS根据Boot Sequence中的顺序，将最前面的存储设备的引导扇区的内容加载到内存中，并跳转到引导程序的第一条指令
* 4. 再通过基于主引导记录类型(MBR/GPT/GUID)来指定的寻址模式(LBA/CHS)来寻找已有的开机引导程序(进入磁盘启动环节)
> 关于MBR与GPT的内容可参考历史文章
* 5. 基于某个类别的主引导记录类型利用分区表将控制权转交给硬盘的某个分区
> 此时在四个主分区里面，只有一个是激活的计算机会读取激活分区的第一个扇区，叫做卷引导记录(Volume Boot Record，缩写为VBR，也可称为分区引导记录，Partition Boot Record，缩写为PBR)
> 卷引导记录的有以下主要作用:
> 寻找激活分区根目录下的grldr(Grub),NTLDR(XP),bootmgr(Win7 above),btldr.mbr(BootLink)等可用于引导的程序
* 6. 执行启动管理器(boot loader)，此时卷引导记录搜索到激活分区中的启动管理器，将控制权交给启动管理器运行
> boot loader是系统预先安装的程序，用以实现由用户选择启动哪一个操作系统
> 启动管理器寻找激活分区中的启动配置数据(如: Win7中的BCD文件、XP中的boot.ini文件)，根据启动配置数据，在显示器上显示多操作系统选择画面
> 然后选择相应的操作系统
> 最后控制权交给操作系统
> Linux环境中，目前最流行的启动管理器是Grub
> 在windows下为启动管理器bootmgr(xp中的ntldr文件)
* 7. 下一步是将控制权转交给操作系统，以此让操作系统的内核首先被载入内存
* 8. 最后实现磁盘内操作系统的启动
**或**
* 1. 由BIOS/UEFI寻找第一个可启动设备(通常为Disk)
* 2. 然后从MBR/GPT/GUID中基于的寻址模式来加载启动程序
* 3. 最终把代码控制权交给GRUB(或其它引导程序)

* 所谓操作系统的引导过程是将存放在硬盘上的静态的操作系统装载到内存中，并开始执行操作系统的过程
* 每一个不同类别的工具都有完全不同的执行逻辑与所执行步骤对应的执行标志，这里先不做过多阐述

---

**相关概念:**

* 引导扇区: 主引导记录(主引导扇区)/全局唯一标识符(全局唯一标识分区表)
> MBR/GPT/GUID
* 磁盘引导程序所基于的寻址模式(LBA/CHS)
* LVM/RAID(逻辑卷管理/磁盘阵列)
* BIOS/UEFI(固件系统)
* 磁盘/磁盘分区所属数据类型/文件系统
* 磁盘映像文件格式
* 磁盘驱动/硬件驱动/设备驱动
* 扩展分区(Extended partition)和逻辑分区(logical partition)
> 扩展引导记录(Extended boot record)缩写为EBR
* MBR/GPT分区表
* 启动管理器(boot loader)

---

**磁盘缓存(Disk Buffer/Disk Cache)相关概述:**

* 用于将下载到的数据先保存于系统为软件分配的内存空间中(这个内存空间被称之为"内存池")
> 当保存到内存池中的数据达到一个程度时，便会将数据保存到硬盘中
> 这样可以减少实际的磁盘操作，有效的保护磁盘免于重复的读写操作而导致的损坏

* 磁盘缓存是为了减少CPU透过I/O读取磁盘驱动器的次数
> 提升磁盘I/O的效率，用一块存储器来存储访问较频繁的磁盘内容
> 因为存储器的访问是电子动作，而磁盘的访问是机械动作，感觉上磁盘I/O变得较为快速

* 普遍的磁盘通常有32MB或64MB缓存，现在市售上128MB与256MB也十分常见
> 旧的硬盘则有8MB或16MB

---

### 参考资料

* CN-磁盘缓存[跳转](https://zh.wikipedia.org/wiki/%E7%A3%81%E7%9B%98%E7%BC%93%E5%AD%98)
> `https://zh.wikipedia.org/wiki/%E7%A3%81%E7%9B%98%E7%BC%93%E5%AD%98`

* CN-阮一峰-计算机是如何启动的?[跳转](http://www.ruanyifeng.com/blog/2013/02/booting.html)
> `http://www.ruanyifeng.com/blog/2013/02/booting.html`

* CSDN-操作系统引导过程[跳转](https://blog.csdn.net/jonathan321/article/details/51987680)
> `https://blog.csdn.net/jonathan321/article/details/51987680`

* CSDN-操作系统引导程序学习笔记[跳转](https://blog.csdn.net/aice_dachong/article/details/50843240)
> `https://blog.csdn.net/aice_dachong/article/details/50843240`

* CSDN-操作系统概念：系统引导过程、引导程序、固件[跳转](https://blog.csdn.net/qq_36328643/article/details/79922425)
> `https://blog.csdn.net/qq_36328643/article/details/79922425`

---

### 补充内容

**硬盘的物理结构描述与图解:**

* 磁盘的物理结构图例-1

<img src="/images/disk-images/磁盘-1.png" width="20%" height="20%">

* 磁道(Track)
* 柱面(Cylinder)
* 扇区(Sector)
* 磁头(Heads)
* 盘片(Platters)
* 每个碟片都有两面，因此也会相对应每碟片有2个磁头

---

* 磁盘的物理结构图例-2

<img src="/images/disk-images/磁盘-6.png" width="20%" height="20%">

* A: 磁道
* B: 扇面
* C: 扇区
* D: 簇(扇区组)
* 在硬盘上定位某一数据记录位置—C扇区，使用了三维定位

---

* 其它磁盘物理结构有关图片

<img src="/images/disk-images/磁盘-2.png" width="20%" height="20%">

<img src="/images/disk-images/磁盘-3.png" width="20%" height="20%">

<img src="/images/disk-images/磁盘-4.png" width="20%" height="20%">

<img src="/images/disk-images/磁盘-5.png" width="20%" height="20%">

---

**图片来源:**

* CN-简书[跳转](https://www.jianshu.com/p/42308db1fcde)
> `https://www.jianshu.com/p/42308db1fcde`

* CN Wiki-GPT[跳转](https://zh.wikipedia.org/wiki/GUID%E7%A3%81%E7%A2%9F%E5%88%86%E5%89%B2%E8%A1%A8)
> `https://zh.wikipedia.org/wiki/GUID%E7%A3%81%E7%A2%9F%E5%88%86%E5%89%B2%E8%A1%A8`

* CN Wiki-磁盘[跳转](https://zh.wikipedia.org/wiki/%E7%A1%AC%E7%9B%98)
> `https://zh.wikipedia.org/wiki/%E7%A1%AC%E7%9B%98`

---



