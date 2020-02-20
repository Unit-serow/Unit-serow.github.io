---
title: X Window-1
date: 2020-02-20 23:31:38
tags: 随笔
categories: [软件,X Window]
---

### X Window System

**概述:**

* X 窗口系统，别称/X11/X
* X以位图方式显示的软件窗口系统
* X能为GUI环境提供基本的框架
* X只是工具包及架构规范，本身并无实际参与运作的实体，所以必须有人依据此标准进行开发撰写
> X只是一个协议(protocal)，这个协议定义一个系统成品所必需具备的功能
> 任何系统能满足此协议及符合Ｘ协会其他的规范，便可称为X
* 标准实现体:X.Org(显示服务器)，XFree86(显示服务器)
* GNOME(显示管理器)和KDE(显示管理器)是以X11窗口系统为基础建构成的
* X的标准实现是X.Org的参考实现
* 基于MIT许可证授权
---
* 最初是1984年麻省理工学院的研究，之后变成UNIX、类UNIX、以及OpenVMS等操作系统所一致适用的标准化软件工具包及显示架构的运作协议
* 最新的参考实现(参考性、示范性的实现体)版本则是X11 Release 7.7(简称：X11R7.7)，时间为2012年6月6日
---
**X的C/S模型**

* X采用C/S的架构模型(Client/Server)
> X的一大特点:网络透明性
> 应用程序("客户端"应用程序)所运行的机器，不一定是用户本地的机器(显示的"服务器")
> X中所提及的"客户端"和"服务器"等字眼用词也经常与人们一般想定的相反
> "服务器"反而是在用户本地端的自有机器上运行，而非是在远程的另一部机器上运行
---
**网络透明性**

* 服务器和客户端之间的通信协议的运作对计算机网络是透明的
> 客户端和服务器可以在同一台计算机上，也可以不是，或许其架构和操作系统也不同，但都能运行
> 客户机和服务器还能够使用安全连接在互联网上安全地通讯

----

**X Terminal**

* X Terminal(X 终端机)
* 作为仅运行X服务器的[^1]瘦客户端(Thin Client)的作用硬件
* 该架构广泛用于为了使多人同时使用同一个大型服务器而构造终端
* X终端搜索网络，使用XDMCP产生允许其运行客户机的主机列表
* 初始主机需要运行X显示管理器
* 专用的X终端机硬件已经于上个世纪被淘汰了
* 在1990年初期也被称为"穷人的UNIX工作站"

[^1]:指的是在客户端-服务器网络体系中的一个基本无需应用程序的计算哑终端

---

### 安装显示服务器/显示管理器(X.org/XFree86-GNOME/Xface)

* X11
* apt源推荐(非必要)
> `$emacs /etc/apt/sources.list`
> `deb http://mirrors.geekbone.org/debian/ sid main contrib non-free`
> `deb-src http://mirrors.geekbone.org/debian/ sid main contrib non-free`
---
> `deb http://debian.cn99.com/debian/ sid main contrib non-free`
> `deb-src http://debian.cn99.com/debian/ sid main contrib non-free`
> `deb http://debian.okey.net/debian-uo/ sid java marillat rareware misc`
---

* 安装依赖项以及`X.org/GNOME`
> `apt-get -y install xbase-clients`
> `apt-get -y install x-window-system-core`
> `apt-get -y install xfonts-base (xfs为字体服务器)`
> `apt-get -y install xserver-xorg*`
> `apt-get -y install fvwm2`
> `apt-get -y install menu`
> `apt-get -y install gnome-core (gnome安装，以gnome为窗口管理器)`
> `apt-get -y install gdm*`
> `apt-get -y install xscreensaver-gnome`或`apt-get -y install xscreensaver*`
> `'*'`为UNIX内标准通配符之一

* 其它(XFCE4/XFREE86)
> `apt-get -y install xfce4`
> `apt-get -y install xserver-xfree86`
> `dpkg-reconfigure xserver-xfree86 (重新配置)`
> `apt-get -y install mozilla-firefox (浏览器安装)`

* 参数`-y`假定对所有的询问选是，不提示
* 可以选择是否添加(安装)中文补丁(一般安装系统的时候就会选择)
* 启动执行startx命令

* 便捷安装:
> `apt-get -y install X Windows System*`
> `apt-get -y install GNOME*`

* 音量错误解决方法
> `apt-get install alsa-base`
> `apt-get install alsa-utils`

---

### 其它概念:

* X Window所关系的概念非常庞大，以至于包含整个UNIX体系的图形化界面的历史与技术

**包含于:**

> X Window 架构
> X Window 拓展
> X Window 显示服务器
> X Window 显示管理器
> X Window 会话管理器
> X Window 窗口管理器(合成/平铺/堆叠)
> X Window 标准
> X Window 应用程序
> X Window 桌面环境

---

### 参考资料:

* X.org官方网站[跳转](https://www.x.org/wiki/)
> `https://www.x.org/wiki/`

* X.org官方文档[跳转](https://www.x.org/wiki/Documentation/)
> `https://www.x.org/wiki/Documentation/`

* X.org镜像源[跳转](https://www.x.org/wiki/Releases/Download/)
> `https://www.x.org/wiki/Releases/Download/`

* X.org获取地址[跳转](https://www.x.org/releases/individual/)
> `https://www.x.org/releases/individual/`

---
