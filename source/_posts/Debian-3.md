---
title: Debian-3
date: 2020-02-23 18:57:21
tags: [GNU/Linux,随笔]
categories: [软件,GNU]
---

## Debian GNU/Linux-3

### Linux 磁盘管理

---

* 本篇文章会不断进行补充

**常见的分区有以下三个:**
* fdisk
* cfdisk
* partman

---

**cfdisk用法**

* 简易分区管理工具
* 这里的磁盘类型是`SCSI`，`IDE`则为`hda`，`SATA`与`NVMe`这里不进行过多赘述
* 具体可以查看`man手册`与`help帮助`指令
* 基本流程:`创建分区->配置文件系统根目录与其它选项(作用/用途)->格式化文件系统->文件系统挂载并使用`

**创建分区:**
1. 键入指令`$cfdisk /dev/sda`
2. 选择任意分区(最好是空白分区，已有分区需要先进行删除)
3. `选择[new选项]->[primary选项]->[指定容量数值(以字节为单位)]`
4. `选择[write选择]->键入[yes保存修改]->选择[quit选项退出工具]`

* 参数说明:
* primary 主分区
* extended 扩展分区

---

**交换分区操作:**

* 格式化交换分区指令(这里将sda1格式化为交换分区)
> `$mkswap /dev/sda1`
* 使用交换分区
> `$swapon [交换分区设备名/交换文件]`
> `$swapon /dev/sda`

* 查看内存信息来检查是否已启用交换分区
> `$free`

* 取消交换分区
> `$swapoff /dev/sda1`

---

**其它概念(交换分区):**

**swap**
* swap的部分内容就是开启了多少交换空间，其空间大小是开启使用的交换分区或者文件大小的总和
* 交换分区可以同时存在多个并可以同时使用
* 同时也可以使用文件格式的交换空间

**交换空间**
* 一般主机系统里会有两个磁盘分区
* 一个是交换空间，另一个则是其它的任何分区
* 第一个分区计划为用于交换空间
* 交换空间又可被称为交换内存空间
* 使用这种文件系统的分区被称为交换分区，用于进行系统过程中的内存交换

---

**格式化分区操作:**

* 将磁盘分区格式化为指定的文件系统
* 有以下几种语法格式:
> `mkfs.ext2/ext3/ext4/xfs等等 /dev/sdaxxx/(指定磁盘)`
> `mkfs.文件系统 [分区或设备名]`
> `mkfs [options] [指定磁盘文件格式] /dev/sdaxxx/(指定磁盘)`
> 参数`-v`，`-t`等等
> 例如:`mkfs -t ext4 /dev/sda3`

---

**磁盘(光盘或设备)挂载:**
* 基本语法格式:
> `mount -o loop [/dev/sdaxxx(指定磁盘)] [/mnt(被挂载目录)]`
> `mount -t ext4(指定磁盘文件系统) /dev/sda4 /mnt`
* 卸载光盘
> `umount /mnt`
> `umount /dev/sda2`

* mount查看磁盘文件系统挂载情况
> 参数`-h`返回容量单位

* mount输出参数说明:
> ro表示只读
> rw为可读可写

---

**查看磁盘文件系统挂载情况:**
> `$df`

---

**磁盘文件系统修复:**
* fsck
> fsck(file system consistency check)
* 是Unix和类Unix系统上用于检查文件系统完整性的工具
* 基本命令格式:
> `fsck -y /dev/sda1(指定磁盘)`

* fuser
> `fuser -m /boot` 输出选项模块对应线程的pid
> `fuser -mk /boot` kill掉所选进程的pid


---

**其它概念:**

* hda一般是指IDE接口的硬盘，hda一般指第一块硬盘，类似的有hdb,hdc等
* sda一般是指SATA接口的硬盘，sda一般指第一块硬盘，类似的有sdb,sdc等
* 现在的内核都会把硬盘，移动硬盘，U盘之类的识别为sdX的形式

---

**参考资料:**

* Debian 分区程序[跳转](https://www.debian.org/releases/wheezy/mips/apcs05.html.zh-cn)
> `https://www.debian.org/releases/wheezy/mips/apcs05.html.zh-cn`

* 从零开始的Linux From Scratch[跳转](http://www.linuxfromscratch.org/lfs/downloads/9.1-rc1/LFS-BOOK-9.1-rc1-NOCHUNKS.html)
> `http://www.linuxfromscratch.org/lfs/downloads/9.1-rc1/LFS-BOOK-9.1-rc1-NOCHUNKS.html`

---

**问题解决方案:**

**1.找不到fdisk指令**

* 查看路径:
> `whereis cfdisk`

* 输出现有PATH变量路径
> `echo $PATH`

* 配置软链接
> `ln -sv [软件所在路径] [PATH所指定路径]`

---

