---
title: Debian GNU/Linux-1
date: 2020-02-18 02:49:28
tags: [随笔,GNU/Linux]
categories: [软件,GNU]
---

### Debian GNU/Linux-1

* 通用软件包管理与操作的解决方案
* 一:`apt-get`一条龙的全自动化解决
* 二:`wget/curl`获取->`dpkg/autoconf`安装->设置环境变量->设置别名
* `apt-get/dpkg/wget/curl`都可用户依赖解决	

---

* 目录:
1. apt-get
2. curl
3. wget
4. dpkg
5. autoconf-configure/make
6. env/export
7. set/declare
8. alias

---

### Debian内软件获取与卸载方法简述

**APT-GET包管理器参数简述**

* 从镜像源仓库拉取软件包并于本地自动配置
> `$apt-get install package_name`

* 联网解决或清理依赖关系
> `$apt-get install -f`

* 刷新本地镜像源仓库索引
> `$apt-get updata`

* 更新本地镜像源仓库与所有可更新软件包
> `$apt-get upgrade`

* 查看软件包依赖
> `$apt-get show`
> `$apt-cache show depends package_name`

* 查看仓库内软件包列表
> `$apt-get search`
> `$apt-cache  search  package_name`

* 卸载软件包及其配置文件
> `$apt purge/apt remove`
> `$apt-get -purge remove package_name`

* 删除软件包备份
> `$apt-get clean`

* 镜像源目录:
> `/etc/apt/sources.list`

* 还有很多用于包管理与镜像管理的软件与程序
> conda,npm等等...

* CentOS体系
> yum/rpm

---

### URL拉取工具

* 拉取所选网页内所有资源，多用于直接从远端仓库拉源码至本地

**CURL**
> `$curl [URL(选项)] [参数(options)]`

**WGET**
> `$wget [URL(选项)] [参数(options)]`
* 参数简述:
> `-r`下载整个网站
> `-c`断点续传
> `-i`批量下载
> `--help/man`

---

### Dpkg

* 用于管理Debian包的工具

* 安装已有包
> `$dpkg -i package_name.deb`

* 安装目录下的所有包
> `$dpkg -R /文件目录`

* 查看软件包安装位置
> `$dpkg -L 软件包`

* 卸载一个包及其配置信息
> `$dpkg -P package_name`

> `--help/man`

---

### 源码包安装与管理

**autotools**

* 保证下载来的源码包已经有makefile和由autoconf生存的configure脚本
* 根据makefile运行configure脚本并选择安装路径
> `$./configure --prefix=/安装目录`
* 用make进行源码编译
> `$make`
* 使用make安装
> `$make install`

* 还有很多参数`--help`或`man`
* 在source内执行make uninstall卸载软件包
* 正常情况下source内的makefile都能写uninstall
* 没有makefile的话看makefile的安装项，挨个删除
* 如果连source被删了的话，那没法了

---

### 解压

* tar -zxvf xxx.tar
* zip xxx.zip
* gzip xxx.gzip

* 解压没什么好说的

---

### 环境变量与自定义变量

**配置环境变量与自定义变量(PATH变量/Shell变量)**

* 系统变量/用户变量

**PATH变量**

* 查看PATH变量列表(内容)
> `$echo $PATH`

* PATH变量的默认优先于用户的可执行程序

* 用export工具向PATH内添加内容
> `export PATH=$PATH:/可执行文件所在目录/`
* 此时添加的是永久变量
* export命令基本格式
> `export [-fnp][变量名称]=[变量设置值]`

* 可执行文件目录说明:
> 可执行文件多存于`/usr/local/bin`与`/usr/bin`内
> `/usr/local/bin`优先于`/usr/bin`
> `/usr/bin`目录用于存放系统预装的可执行程序文件
> `/usr/local/bin`目录用于存放用户的可执行的文件，系统升级会覆盖此目录

---

* 用set工具添加环境变量与自定义变量
* set用于添加session(会话)级别环境变量

* 语句形式
> `set PATH=/usr/local/xxx/bin`

* 或用declare定义新变量:
> `declare 变量名='变量值'`

---

**env/export/set/declare简述**

* env 和 export 显示环境变量
> env 显示系统级别的环境变量，不显示自定义
> export 功能与env相同，只不过会根据变量名进行排序

* set 和 declare 显示环境变量和自定义变量
> set 显示用户级别的环境变量，显示自定义
> declare 显示所有级别的变量

* export用于管理env，set用于管理declare

* set 用来显示本地变量
* env 用来显示环境变量
* export 用来显示和设置环境变量

* set 显示当前shell的变量，包括当前用户的变量
* env 显示当前用户的变量
* export 显示当前导出成用户变量的shell变量

---

* 清除用户级别环境变量
> `unset 变量名`

**变量所在目录**

* 普通用户
> `~/home/.bashrc`

* root用户
> `~/.bashrc`
> `~/etc/profile`

* 权限足够时可以直接对其进行修改与管理

* 其他概念
* `~/.bashrc`
* `~/.bash_profile`
* `~/etc/profile`
* `~/etc/environment`

**usr全称:Unix System Resource**

---

### 别名

* 使用alias工具对指令设置别名

* 基本格式:
> `$alias[别名]=[指令名称]`

---
