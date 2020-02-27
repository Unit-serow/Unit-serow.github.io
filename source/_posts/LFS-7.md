---
title: LFS-7
date: 2020-02-27 16:53:15
tags: [GNU/Linux,随笔]
categories: [软件,GNU]
---

### LFS-7

* 内核编译等内容
* 有关GRUB的内容会再做补充

---

### 相关指令(通用执行逻辑简述)

* 清理编译所处环境的内核依赖树
> `$makemrpoper`

---

* 通过菜单驱动的界面配置内核
* BLFS包含一些有关LFS外部软件包的特定内核配置要求的信息[BLFS-kernel](http://www.linuxfromscratch.org/blfs/view/svn/longindex.html#kernel-config-index)
* 基本语法
> `make LANG=<host_LANG_value> LC_ALL= menuconfig`

* 参数含义:
> make将语言环境设置建立为主机上使用的语言环境设置(这个参数建立主机上使用的locale设置)
> UTF-8 的linux文本控制台上的菜单配置ncurses 接口线图需要这个值
> 确保用主机上的`$LANG变量代替<host_LANG_value>(还可以说是用主机中变量<host_LANG_value>的值替换$LANG)`
> 如果主机没有设置，还可以使用`$LC_ALL或$LC_CTYPE`的值代替

* 另外在某一些场合使用`$make oldconfig`可能更合适
> 更多信息可参考README文件

* 还有一种方法，可以跳过配置内核的步骤
> 直接把宿主系统里的内核配置文件`.config`(如果存在的话)复制到解压后的linux-2.6.32.8目录
> FLS官方说明这里不推荐这么去做
> 考察全部的配置菜单并从头开始创建内核配置是更好的办法

---

* 编译内核映像和所选模块
> make

* 参数说明
> 如果使用内核模块，可能需要`/etc/modprobe.d`目录中的模块配置
> 关于模块和内核配置的信息请参考 Section 7.9内的LFS 系统的设备和模块处理内容和linux-2.6.32.8/Documentation目录的内核文档
> `modprobe.conf(5)`也可能有用

---

* 如果内核配置使用模块，执行模块安装指令:
> `make modules_install`

* 当内核编译完成后，还需要一些步骤来完成安装
* 比如需要把一些文件拷贝到/boot目录

---

* 内核镜像文件所在的路径因所处主机使用的平台不同而不同
* 下面的文件名可以更改为符合本地主机的配置
* 但为了与下一节描述的启动过程的自动安装兼容，文件名的词干应该是vmlinux

* x86平台上运行以下命令:
> `cp -v arch/x86/boot/bzImage /boot/vmlinux-2.6.32.8-lfs-6.6`
* System.map是内核的符号文件
* 它映射了内核API中每个函数的入口， 以及正在运行内核的数据结构的地址
* 在调查内核问题时，使用它作为一种资源， 运行以下的命令安装此文件:
> `cp -v System.map /boot/System.map-2.6.32.8`
* 上面`make menuconfig`这一步产生的内核配置文件`.config`包含了刚刚编译的内核的所有配置选项
* 最好保留这个文件以备将来参考:
> `cp -v .config /boot/config-2.6.32.8`
* 安装Linux内核文档:
> `install -d /usr/share/doc/linux-2.6.32.8`
> `cp -r Documentation/* /usr/share/doc/linux-2.6.32.8`

---

**配置Linux模块装载顺序:**

* 需要创建`/etc/modprobe.d/usb.conf`文件
> 以便如果将USB驱动(`ehci_hcd， ohci_hcd 和uhci_hcd`)编译成模块时，它们会按正确的顺序装载
> 为了避免在启动时出现警告，`ehci_hcd`必须在`ohci_hcd和uhci_hcd`之前装载

* 通过运行下面的命令来建立一个新文件/etc/modprobe.d/usb.conf:
```
install -v -m755 -d /etc/modprobe.d
cat > /etc/modprobe.d/usb.conf << "EOF"
# Begin /etc/modprobe.d/usb.conf

install ohci_hcd /sbin/modprobe ehci_hcd ; /sbin/modprobe -i ohci_hcd ; true
install uhci_hcd /sbin/modprobe ehci_hcd ; /sbin/modprobe -i uhci_hcd ; true

# End /etc/modprobe.d/usb.conf
EOF
```

---

**注意事项:**
* 重要的一点是要注意到内核源码目录里的文件所有者不是root
> 只要是用 root(像在chroot环境里做的那样)用户解压软件包，解压出来的文件的用户和组ID是这个软件包打包者计算机上的用户和组ID
> 对于其它软件包， 这通常不是问题， 因为安装完这些软件包之后源码目录就删除了
> 但是 Linux 内核源码树常常会保存很长的时间， 这样就有可能打包者的用户 ID 和您计算机上某个用户的 ID 相同
> 从而让您计算机上的这个用户获得了内核源码的写权限

* 如果准备保留内核源代码，在`linux-2.6.32.8`目录上执行`chown -R 0:0`命令以确保全部文件的所有者是`root`

* 一些内核文档建议建立一个从`/usr/src/linux`指向源码目录的符号链接
> 这只是一个对 2.6 以前版本内核的特殊要求，并且在 LFS 系统上是不允许这样做的
> 因为基本的LFS系统完成以后，安装其他软件包时可能会因此而引起问题

* 系统include目录中的头问题件应该总是保持Glibc编译时的那个版本
> 这也是Linux内核tar包中的干净的头文件
> 因而，它们绝不要被替换成原始的内核头文件和其他干净的头文件

---

### 参考文献:

* LFS-v6.3[跳转](http://www.linuxfromscratch.org/lfs/view/6.3/)
> `http://www.linuxfromscratch.org/lfs/view/6.3/`

* LFS-v9.3 重新启动系统[跳转](http://www.linuxfromscratch.org/lfs/view/6.3/chapter09/reboot.html)
> `http://www.linuxfromscratch.org/lfs/view/6.3/chapter09/reboot.html`

* CSDN参考资料[跳转](https://blog.csdn.net/Sugar_girl/article/details/78713316)
> `https://blog.csdn.net/Sugar_girl/article/details/78713316`

* LFS内核配置全面信息[跳转](http://www.linuxfromscratch.org/hints/downloads/files/kernel-configuration.txt)
> `http://www.linuxfromscratch.org/hints/downloads/files/kernel-configuration.txt`

* LFS-v6.3-第八章第三节[跳转](http://www.linuxfromscratch.org/lfs/view/6.3/chapter08/kernel.html)
> `http://www.linuxfromscratch.org/lfs/view/6.3/chapter08/kernel.html`

* Beyond Linux From Scratch (System V Edition) - Version 2020-02-27[跳转](http://www.linuxfromscratch.org/lfs/view/6.3/chapter08/kernel.html)
> `http://www.linuxfromscratch.org/blfs/view/svn/longindex.html#kernel-config-index`

---

