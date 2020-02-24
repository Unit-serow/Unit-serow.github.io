---
title: Linux Containers/LXC-1
date: 2020-02-24 16:32:34
tags: [GNU/Linux,随笔]
categories: [软件,虚拟化]
---

## Linux Containers/LXC-1

**相关内容:**
* LXC(Linux Containers)
* linux内核映射文件
* 文件映射

---

### LXC(Linux Containers)

**概述:**
* 其名称来自Linux软件容器(Linux Containers)的缩写
* 是一种操作系统层虚拟化（Operating system–level virtualization)技术
* 作用是为Linux内核容器功能的一个用户空间接口

---

### 技术实现

1. **实现方法:**

* 在Linux内核中，提供了cgroups功能，来达成资源的区隔化
> 它同时也提供了名称空间区隔化的功能，使应用程序看到的操作系统环境被区隔成独立区间，包括行程树，网络，用户id，以及挂载的文件系统
> 但是cgroups并不一定需要引导任何虚拟机
> LXC利用cgroups与名称空间的功能，提供应用软件一个独立的操作系统环境
> LXC不需要Hypervisor这个软件层，软件容器(Container)本身极为轻量化，提升了创建虚拟机的速度
> 软件Docker被用来管理LXC的环境
---
* 执行流程简述:
> 它将应用软件系统打包成一个软件容器(Container)，内含应用软件本身的代码，以及所需要的操作系统核心和库
> 透过统一的名字空间和共享API来分配不同软件容器的可用硬件资源，创造出应用程序的独立沙箱运行环境
> 从而使得Linux用户可以容易的创建和管理系统或应用容器

---

2. **具体实现:**

* 当前的LXC使用下列内核功能来控制进程:
> 内核名字空间(进程间通信，uts，mount，pid，network和user)
> AppArmor和SELinux配置
> Seccomp策略
> chroot(使用`pivot_root`)
> Kernel Capibilities
> 控制组(cgroups)

* 因此，LXC通常被认为介于“加强版”的chroot和完全成熟的虚拟机之间的技术。LXC的目标是创建一个尽可能与标准安装的Linux相同但又不需要分离内核的环境

---

3. **具体使用:**
* Proxmox VE:它直到4.0版才使用LXC技术，在此之前的版本都是使用OpenVZ技术
* Docker:它在0.9版之前都是使用LXC技术，但在0.9版之后，已不再是唯一且默认的运行环境

---

### 内存映射文件

**概述:**
* 内存映射文件(Memory-mapped file)，或称"文件映射"与"映射文件"
* 是一段虚内存逐字节对应于一个文件或类文件的资源，使得应用程序处理映射部分如同访问主内存

---

**内存映射文件分为以下两种:**
* Persisted
> Persisted文件与硬盘文件相关联，当关闭内存映射时，数据被写入对应的硬盘文件中
> 适合于很大的文件
* Non-persisted
> Non-persisted文件并不关联于硬盘文件。当关闭内存映射文件，所有数据被抛弃
> 适用于创建进程间通信的共享内存

**作用:**
1. 最常见用途是绝大多数操作系统(包括Microsoft Windows与Unix-like系统)用于加载进程
2. 另一个用途是多个进程的共享内存
3. 第三个用途是对大文件的读写

**优势:**
1. 主要用处是增加I/O性能，特别是用于大文件
2. 对于小文件，内存映射文件会导致碎片空间浪费，因为内存映射总是要对齐页边界，这起码是4 KiB
> 因而一个5 KiB文件将会映射占用8 KiB内存，浪费了3 KiB内存
3. 访问内存映射文件比直接文件读写要快几个数量级

**缺点(弊端):**
1. 内存映射文件需要在进程的占用一块很大的连续逻辑地址空间
2. 对于Intel的IA-32的4 GiB逻辑地址空间，可用的连续地址空间远远小于`2---3GiB`
> 相关联的文件的I/O错误(如可拔出驱动器或光驱被弹出，磁盘满时写操作等)的内存映射文件会向应用程序报告SIGSEGV/SIGBUS信号(POSIX环境)
> 或`EXECUTE_IN_PAGE_ERROR`结构化异常(Windows环境)
> 但通常的内存操作是无需考虑这些异常的
3. 有内存管理单元(MMU)才支持内存映射文件

---

### 参考文献

* 官方网站[跳转](https://linuxcontainers.org/)
> `https://linuxcontainers.org/`

* LXC官方文档[跳转](https://linuxcontainers.org/lxc/introduction/)
> `https://linuxcontainers.org/lxc/introduction/`

---

**以下内容参考自中文维基:**

* 虚拟内存[跳转](https://zh.wikipedia.org/wiki/Category:%E8%99%9A%E6%8B%9F%E5%86%85%E5%AD%98)
> `https://zh.wikipedia.org/wiki/Category:%E8%99%9A%E6%8B%9F%E5%86%85%E5%AD%98`

* 磁盘文件系统[跳转](https://zh.wikipedia.org/wiki/Category:%E7%A3%81%E7%9B%98%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F)
> `https://zh.wikipedia.org/wiki/Category:%E7%A3%81%E7%9B%98%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F`

* Linux容器化[跳转](https://zh.wikipedia.org/wiki/Category:Linux%E5%AE%B9%E5%99%A8%E5%8C%96)
> `https://zh.wikipedia.org/wiki/Category:Linux%E5%AE%B9%E5%99%A8%E5%8C%96`

* Linux内核功能[跳转](https://zh.wikipedia.org/wiki/Category:Linux%E5%86%85%E6%A0%B8%E5%8A%9F%E8%83%BD)
> `https://zh.wikipedia.org/wiki/Category:Linux%E5%86%85%E6%A0%B8%E5%8A%9F%E8%83%BD`

* 操作系统层虚拟化[跳转](https://zh.wikipedia.org/wiki/%E4%BD%9C%E6%A5%AD%E7%B3%BB%E7%B5%B1%E5%B1%A4%E8%99%9B%E6%93%AC%E5%8C%96)
> `https://zh.wikipedia.org/wiki/%E4%BD%9C%E6%A5%AD%E7%B3%BB%E7%B5%B1%E5%B1%A4%E8%99%9B%E6%93%AC%E5%8C%96`

* DevOps[跳转](https://zh.wikipedia.org/wiki/DevOps)
> `https://zh.wikipedia.org/wiki/DevOps`

* 虚拟化技术(Virtualization)[跳转](https://zh.wikipedia.org/wiki/%E8%99%9B%E6%93%AC%E5%8C%96)
> `https://zh.wikipedia.org/wiki/%E8%99%9B%E6%93%AC%E5%8C%96`

---

