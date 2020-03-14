---
title: VPS/KVM-1
date: 2020-03-05 04:28:57
tags: [随笔,GNU/Linux]
categories: [软件,虚拟化]
---

<center><strong>VPS/KVM简要概述</strong></center>

<!-- more -->

## VPS/KVM-1

---

### 虚拟专用服务器 (Virtual private server)

**简述:**

* 简称VPS
* 由容器技术或虚拟机技术实现
* 在容器或虚拟机中，每个VPS都拥有独立的公网IP，操作系统，磁盘空间，内存与处理器资源
> 同时进程与系统配置之间也相互隔离
> 目的就是为了让用户和应用程序在同一个主机上模拟出完全不同，独立且相互隔离的资源占用与控制
> 以此让VPS可以完全拥有独立服务器的所有功能
* 并且VPS为用户提供了管理配置的自由
* VPS多用于企业虚拟化于IDC资源租用
* VPS拥有完全的独立性，包括可以在容器内自行安装任何程序与其它对于虚拟硬件的操作
> 远端服务器->容器/虚拟机->容器/虚拟机->用户

---

### 基于内核的虚拟机 (Kernel-based Virtual Machine)

**简述:**

* 可简称为KVM
* 是一种用于Linux内核中的虚拟化基础设施，可将Linux内核转化为一个虚拟机监视器
* KVM于2007年2月5日被导入Linux 2.6.20核心中，基于C
* KVM需要支持硬件虚拟化拓展特性的处理器
* 对于操作系统支持的范围较为广泛
* 基于多个GNY协议授权
> 包括KVM内核模块: GPL v2
> KVM用户模块: LGPL v2
> QEMU虚拟CPU内核库(libqemu.a)和QEMU PC系统模拟器: LGPL
> Linux用户模式QEMU模拟器: GPL
> BIOS文件(bios.bin，vgabios.bin和vgabios-cirrus.bin): LGPL v2或更新
* KVM现由保罗·邦齐尼(Paolo Bonzini)维护
* KVM 支持VirtIO半虚拟化技术-平行虚拟化技术(paravirtualization)

---

**内部结构:**

* KVM提供抽象的设备，但不模拟处理器
* 它开放了`/dev/kvm`接口，供使用者模式的主机使用:
1. 设置客户虚拟机的地址空间
> 宿主机同样也需用户可用于引导进主操作系统的固件镜像(通常为模拟PC时的自定义BIOS)
2. 为客户机模拟I/O
3. 将客户机的视频显示映射回系统宿主机上

* 在Linux上，QEMU版本0.10.1及更新版就是一个用户层主机
> QEMU使用KVM以近乎原生的速度虚拟化客户机，若无KVM的话则将仅使用软件模拟
* KVM内部使用SeaBIOS作为对16位x86 BIOS的开源模拟

* KVM/QEMU环境的高级概述:

<img src="/images/KVM-1.png" width="40%" height="40%">

---

**相关GUI(图形化管理)工具:**

* Kimchi – 网页版KVM虚拟化管理工具
* Virtual Machine Manager – 支持创建、编辑、开始于关闭基于KVM的虚拟机，同时也支持对宿主之间的实时或冷拖拽虚拟机迁移
* Proxmox虚拟环境 – 一项开源的虚拟化管理包，包括KVM与LXC
> 同时它还有裸机安装器、网页版远程管理界面、HA集群堆栈、统一存储、柔性网络及可选的商业支持
* OpenQRM – 用于管理不同数据中心基础设施的平台
* GNOME 机柜 – Linux上用于管理libvirt客户机的Gnome界面
* oVirt – 用于管理基于libvirt的KVM开源工具

---

**相关概念(关键字):**

* VPS
* KVM
* Virtual
* CN2

---

### 参考资料

* EN-Redhat-KVM官方网站[跳转](https://www.linux-kvm.org/page/Main_Page)
> `https://www.linux-kvm.org/page/Main_Page`

* CN-CN2线路是什么，有哪些CN2线路的VPS[跳转](https://blog.sprov.xyz/2019/04/09/what-is-cn2-vps/#_CN2)
> `https://blog.sprov.xyz/2019/04/09/what-is-cn2-vps/#_CN2`

**维基百科参考内容:**

* CN-虚拟主机[跳转](https://zh.wikipedia.org/wiki/%E8%99%9A%E6%8B%9F%E4%B8%BB%E6%9C%BA)
> `https://zh.wikipedia.org/wiki/%E8%99%9A%E6%8B%9F%E4%B8%BB%E6%9C%BA`

* CN-虚拟专用服务器[跳转](https://zh.wikipedia.org/wiki/%E8%99%9A%E6%8B%9F%E4%B8%93%E7%94%A8%E6%9C%8D%E5%8A%A1%E5%99%A8)
> `https://zh.wikipedia.org/wiki/%E8%99%9A%E6%8B%9F%E4%B8%93%E7%94%A8%E6%9C%8D%E5%8A%A1%E5%99%A8`

* CN-服务器[跳转](https://zh.wikipedia.org/wiki/Category:%E6%9C%8D%E5%8A%A1%E5%99%A8)
> `https://zh.wikipedia.org/wiki/Category:%E6%9C%8D%E5%8A%A1%E5%99%A8`

* CN-虚拟化[跳转](https://zh.wikipedia.org/wiki/%E8%99%9B%E6%93%AC%E5%8C%96)
> `https://zh.wikipedia.org/wiki/%E8%99%9B%E6%93%AC%E5%8C%96`

* CN-硬件虚拟化[跳转](https://zh.wikipedia.org/wiki/%E7%A1%AC%E4%BB%B6%E8%99%9A%E6%8B%9F%E5%8C%96)
> `https://zh.wikipedia.org/wiki/%E7%A1%AC%E4%BB%B6%E8%99%9A%E6%8B%9F%E5%8C%96`

* CN-KVM-基于内核的虚拟机[跳转](https://zh.wikipedia.org/wiki/%E5%9F%BA%E4%BA%8E%E5%86%85%E6%A0%B8%E7%9A%84%E8%99%9A%E6%8B%9F%E6%9C%BA)
> `https://zh.wikipedia.org/wiki/%E5%9F%BA%E4%BA%8E%E5%86%85%E6%A0%B8%E7%9A%84%E8%99%9A%E6%8B%9F%E6%9C%BA`

---

### Shadowsocks

* 境外KVM类型的VPS大约360RMB/年(美国)
> 最便宜的

* 官网地址: https://shadowsocks.org/en/index.html
* 仓库地址: https://github.com/shadowsocks

---

**可用参考:**

* CN-Github-SS教程
> https://github.com/233boy/ss/wiki/Shadowsocks%E6%90%AD%E5%BB%BA%E8%AF%A6%E7%BB%86%E5%9B%BE%E6%96%87%E6%95%99%E7%A8%8B
> https://ssr.tools/252

* 搬瓦工 (Bandwagon Host)
> VPS供应商，支持支付宝支付
> https://bwh88.net/cart.php?gid=1
> https://bwg.net/

* CN2: `https://blog.sprov.xyz/2019/04/09/what-is-cn2-vps/#_CN2`

---

* shadowsocks server
> https://github.com/shadowsocksr-backup/shadowsocksr
> `$ apt-get install python-pip`
> `$ pip install shadowsocks`

* client
> https://github.com/Jigsaw-Code/outline-client/
> https://github.com/shadowsocks/shadowsocks-qt5/wiki/Installation
> https://shadowsocks.org/en/download/clients.html

**Debian**

* 软件源
> https://github.com/debiancn/repo

* 直接拉取shadowsocks-qt5
> `$ apt-get install shadowsocks-qt5 -y`

* 软件源配置:
```
$ echo "deb https://repo.debiancn.org/ testing main" | sudo tee /etc/apt/sources.list.d/debiancn.list;
$ wget https://repo.debiancn.org/pool/main/d/debiancn-keyring/debiancn-keyring_0~20161212_all.deb -O /tmp/debiancn-keyring.deb;
$ sudo apt install /tmp/debiancn-keyring.deb;
$ sudo apt update;
$ rm /tmp/debiancn-keyring.deb;
```

* 清理源指令:
```
$ sudo apt purge debiancn-keyring;
$ sudo rm -f /etc/apt/sources.list.d/debiancn.list;
$ sudo apt update;
```

---



