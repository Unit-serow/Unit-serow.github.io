---
title: GNU-LFS-3-3
date: 2020-03-01 22:10:58
tags: [随笔,GNU/Linux]
categories: [软件,GNU]
---

## GNU-LFS-3-3

* 系统转换过程与细节描述

---

**文案说明:**

* 本篇文案用于描述目标系统环境的最基本配置与对从临时系统进入到目标系统的各种细节的描述
* 参考文献及版本为LFS-v6.2/v6.3
* 描述主体为LFS-v6.3，LFS-v6.2会有特别标注
* LFS-v6.2和LFS-v6.3的内容与执行语句通常没有本质上的区别
> 多数都只是执行顺序或者深层的处理逻辑不同
> 但大体非常相似
* 多数指令在目标主机的chroot环境下进行

**目录简述:**

* 系统清理
* 虚拟文件系统
* chroot环境
* 标准文件系统(FHS标准)
* 用户与用户组的基本配置
* 参考资料

---

### 系统清理

**临时主机的系统清理**

* 删除已经安装的可执行程序和库文件当中的调试符号，以节约空间(大约70 MB)
> `$ strip --strip-debug /tools/lib/*`
> `$ strip --strip-unneeded /tools/{,s}bin/*`
* 命令会跳过大约20个文件，报告不能识别这些文件格式
> 其中大多数是脚本而不是二进制文件
* 这里需要注意的一点是千万不要在库文件上使用`--strip-unneeded`，否则会破坏其静态版本
> 如果已经是过去时了的话，就得从头开始编译全部的工具链软件包了

* 删除相关文档文件(info，man)，会节约20 MB
> `$ rm -rf /tools/{info,man}`

---

* 到目前为止，临时工具链已制作完毕
* 这一阶段开始进入目标主机环境

* 从现在开始不需要lfs用户来制作系统了
* 退出lfs用户
> `$ exit`

* 此时为root用户环境，改变必要文件的权限与所有者
* 一部分的原因是为了避免不必要的安全方面所产生的问题
* 将$LFS/tools目录以及其中文件的所有者改为root用户
> `$ chown -R root:root $LFS/tools`

* 这里说明一下:
> 建立LFS系统的时候，在创建`/etc/passwd`文件时
> 添加的user ID和group ID是与宿主系统的user ID和group ID相同的lfs用户

---

### 虚拟文件系统

**挂载虚拟文件系统**

* 为虚拟内核文件系统建立挂载目录(dev,proc,sys)
> `$ mkdir -pv $LFS/{dev,proc,sys}`

* 创建初始设备节点(创建两个目标系统所必须的设备文件)
> `$ mknod -m 600 $LFS/dev/console c 5 1` 
> `$ mknod -m 666 $LFS/dev/null c 1 3`

* 具体说明:
> 内核在引导时要求某些设备节点必须存在(特别是console和null)
> 这些设备节点必须创建在 硬盘上才能使得内核在udev尚未启动之前就可以使用它们
> 此外还有当Linux以`init=/bin/bash`启动

* 挂载并填充/dev目录(LFS-v6.2)
> `$ mount --bind /dev $LFS/dev`

*  具体说明:
> LFS-v6.2推荐的向`/dev`目录填充设备的方法是在`/dev`上挂载一个虚拟文件系统(比如	tmpfs)
> 然后在设备被检测到或被访问到的时候(通常是在系统引导的过程中)动态创建设备节点
> 既然现在新的系统尚未被引导，那么就有必要通过手工挂载和填充`/dev`目录
> 这可以通过绑定挂载宿主系统的`/dev`目录
> 绑定挂载是一种特殊的挂载方式，允许本地主机上的当前用户创建一个目录或者是挂载点的镜像到其他的地方

* 挂载虚拟内核文件系统
> `$ mount -v --bind /dev $LFS/dev`
> `$ mount -vt devpts devpts $LFS/dev/pts` 
> `$ mount -vt tmpfs shm $LFS/dev/shm`
> `$ mount -vt proc proc $LFS/proc` 
> `$ mount -vt sysfs sysfs $LFS/sys`

---

* 在进入chroot环境之前，可以将`lfs-sources/`里面所有源码包复制到`$LFS/sources/`目录中
* 这么做会让后面在构建目标系统的时候使用源代码变得更方便
> `$ cp -a /lfs-sources/* $LFS/sources/`

---

### chroot环境

**进入chroot环境**

* Chroot到目标系统的目录下，以便不受主系统的影响来制作目标系统 

```
$ chroot "$LFS" /tools/bin/env -i \ 
HOME=/root TERM="$TERM" PS1='\u:\w\$ ' \ 
PATH=/bin:/usr/bin:/sbin:/usr/sbin:/tools/bin \ 
/tools/bin/bash --login +h
```

**参数说明:**
* `env`命令的`参数-i`的作用是清除所有chroot环境变量
> 后面是重新设定HOME,TERM,PS1, PATH等变量的值
* `TERM=$TERM`设定虚拟根环境中的TERM的值与chroot外面的一样
> 这个值是让像vim和less之类的程序可以正确操作
> 如果还需要重新设置其它的值，如CFLAGS或CXXFLAGS，这里是个不错的位置

---

* 从这里开始，不再需要LFS环境变量了，因为所有的工作都被限制在LFS文件系统里面
> 这是由于已经告诉了Bash shell $LFS 是现在的根目录(`/`)
> 注意，这里`/tools/bin`位于PATH的最后面
> 也就是说当软件包的最终版本安装之后就不再使用临时工具了
> 为了使shell无法记住可执行二进制代码的位置，需要通过使用`+h参数`关闭bash的散列功能

* 此时bash提示符会显示: `I have no name!`这是正常的，因为`/etc/passwd`还没有创建

---

### 标准文件系统

**创建符合FHS标准的Unix文件系统**

**创建系统目录结构(FHS标准目录树):**

> `$ mkdir -pv /{bin,boot,etc/opt,home,lib,mnt,opt}`
> `$ mkdir -pv /{media/{floppy,cdrom},sbin,srv,var}` 
> `$ install -dv -m 0750 /root` 
> `$ install -dv -m 1777 /tmp /var/tmp` 
> `$ mkdir -pv /usr/{,local/}{bin,include,lib,sbin,src}`
> `$ mkdir -pv /usr/{,local/}share/{doc,info,locale,man}`
> `$ mkdir -pv /usr/{,local/}share/{misc,terminfo,zoneinfo}` 
> `$ mkdir -pv /usr/{,local/}share/man/man{1..8}` 

```
$ for dir in /usr /usr/local; do
ln -sv share/{man,doc,info} $dir
done
```

> `$ mkdir -pv /var/{lock,log,mail,run,spool}`
> `$ mkdir -pv /var/{opt,cache,lib/{misc,locate},local}`

---

**创建必需的文件与符号连接**

* 一些程序使用固化的路径(`hard-wired paths`)指向一些目前还不存在的程序上
* 为了兼容这些程序，可以创建一些符号链接
* 然后在软件安装之后用实际文件进行替代

**创建必要的符号链接:**

> `$ ln -sv /tools/bin/{bash,cat,echo,grep,pwd,stty} /bin`
> `$ ln -sv /tools/bin/perl /usr/bin`
> `$ ln -sv /tools/lib/libgcc_s.so{,.1} /usr/lib` 
> `$ ln -sv /tools/lib/libstdc++.so{,.6} /usr/lib` 
> `$ ln -sv bash /bin/sh` 
> `$ touch /etc/mtab`

---

### 用户与用户组的基本配置

**配置必要的用户组**

* 以下区块为LFS-v6.2独有

* 一个常规的Linux系统在`/etc/mtab`中有一个已挂载文件系统的列表正常情况下
* 这个文件 在我们挂载一个新的文件系统的时候会被创建
* 因为从此开始在chroot环境下不会再挂载任何文件系统
* 所以需要人为的为那些用到`/etc/mtab`的程序创建一个空文件
> `$ touch /etc/mtab`

* 为了让`root用户`可以登录而且`用户名root`可以被识别
* 在这里需要创建相应的`/etc/passwd`和`/etc/group`文件

```
$ cat > /etc/passwd << "EOF"
root:x:0:0:root:/root:/bin/bash 
EOF
```

* 此时root的真正密码将在后面设置(`"x"`在这里只是一个占位符)

---

* 使用以下命令创建/etc/group文件(LFS-v6.2):

```
$ cat > /etc/group << "EOF"
root:x:0: 
bin:x:1: 
sys:x:2: 
kmem:x:3: 
tty:x:4: 
tape:x:5: 
daemon:x:6: 
floppy:x:7:
disk:x:8: 
lp:x:9: 
dialout:x:10: 
audio:x:11: 
video:x:12: 
utmp:x:13: 
usb:x:14: 
cdrom:x:15: 
EOF
```

* 在LFS-v6.2这里创建的用户组并不是某个标准所要求的部分
> 只是因为在随后`Udev配置`将要用到而以

---

**创建`root`及`nobody用户`和必要的组(LFS-v6.3):**

```
$ cat > /etc/passwd << "EOF" 
root:x:0:0:root:/root:/bin/bash 
nobody:x:99:99:Unprivileged User:/dev/null:/bin/false 
EOF
```
 
```
$ cat > /etc/group << "EOF" 
root:x:0: 
bin:x:1: 
sys:x:2: 
kmem:x:3: 
tty:x:4: 
tape:x:5: 
daemon:x:6: 
floppy:x:7:
disk:x:8: 
lp:x:9: 
dialout:x:10: 
audio:x:11: 
video:x:12: 
utmp:x:13: 
usb:x:14: 
cdrom:x:15: 
mail:x:34: 
nogroup:x:99: 
EOF
```

---

* 因为完整的Glibc在目标系统中已经安装
* 而且`/etc/passwd`和`/etc/group`文件也已创建
* 所以用户名和组名现在可以开始使用了
* 重新加载bash，以使root用户起效
> `$ exec /tools/bin/bash --login +h`

* 参数说明:
>`参数+h`用于告诉bash不能使用其内部哈希表查找路径

---

* 程序 login, agetty, init(还有其它一些程序)使用一些日志文件来记录信息
* 比如谁在什么时候登录了系统等等
* 然而如果这些日志文件不存在，这些程序则无法写入
* 下面初始化这些日志文件，并设置适当的权限:

> `$ touch /var/run/utmp /var/log/{btmp,lastlog,wtmp}`
> `$ chgrp -v utmp /var/run/utmp /var/log/lastlog` 
> `$ chmod -v 664 /var/run/utmp /var/log/lastlog`

* 目录作用明细:
> `/var/run/utmp`记录着现在登录的用户
> `/var/log/wtmp`记录所有的登录和退出
> `/var/log/lastlog`记录每个用户最后的登录信息
> `/var/log/btmp`记录错误的登录尝试

---

* 此时就已经完成了对目标主机的基础配置
* 同时已经进入目标主机的标准环境了
* 一下步即开始对目录主机进行程序编译与配置
* 进入源代码目录与设置LFS变量
> `$ cd /sources`
> `$ export LFS=/sources`

---

### 参考资料

* 官方-EN-LFS-v6.2
* 官方-EN-LFS-v6.3
* 金步国-CN-LFS-v6.2
* 孙海勇-CN-LFS-v6.3

---



