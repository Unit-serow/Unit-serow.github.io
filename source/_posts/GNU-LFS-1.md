---
title: GNU-LFS-1
date: 2020-02-28 23:31:21
tags: [GNU\Linux,随笔]
categories: [软件,GNU]
---

### LFS-1

* 参考资料为CN-[LFS-BOOK(v9.0)]-PDF版

---

**本地主机环境一览:**
* 原主机环境准备
* 主机内存(RAM)为4GB
* 主机磁盘为30GB
* CPU为4核-2.2GHZ
* 本地主机硬盘接口类型为SCSI
* 磁盘分区表类型为MBR(GPT/GUID不做阐述)
* 磁盘启动引导类型为BIOS(UEFI不做阐述)
* CD使用LFS-liveCD-v6.3(2007)

---

### 1.0.0-1.2.7

**1.0.0**
* 使用cfdisk工具对原主机进行分区(也可以使用fdisk工具进行分区操作)
> `$cfdisk /dev/sda`

**1.1.0 格式化磁盘分区**
* Swap分区(swap)
> `$mkswap /dev/<yyy>`
> `$mkswap /dev/sda1`

* LFS分区(ext)
> `$mkfs -v -t ext4/ext3 /dev/<xxx>`
> `$mkfs.ext4/ext3 /dev/sda2`
> `$mkfs -v -t ext3 /dev/sda2`

* 格式化为ext3文件系统
> `mke2fs -jv /dev/<xxx>`

**相关实例与指令具体说明:**
* 前者为标准格式，后者为实例
* 在原主机磁盘上创建新分区
* 由于是LFS官方提供的liveCD，所以此时的原主机没有任何分区
* 这里创建两个本地的主分区: /dev/sda1用于交换分区(swap)，/dev/sda2用作目标主机制作环境，分区文件格式为ext3(或ext3/ext4等等)
* 存储容量分别是7000B与530000B(拟定，因本地主机的处理器指令集位数问题，实际情况会发生细微变动)

---

**1.2.0 设置LFS所处目录的系统变量**

* 因为整个实现过程需要多次用到LFS系统的目录，所以先将LFS系统目录设置为LFS变量(变量名自拟，这里为LFS，即$LFS)
* 因为这里将要把LFS分区挂载到/mnt目录中，所以可以将LFS系统目录建立到/mnt目录内，以下指令直接创建环境变量:
> `$export LFS=/mnt/lfs`

**1.2.1 将新分区(LFS系统分区)进行挂载**

* 挂载的目是访问所被挂载的分区，上一步中将分区所在目录设为了$LFS变量所指向的地址
* 创建挂载点
> `mkdir -pv $LFS`
* 挂载LFS分区及其文件系统(文件可以自动识别，即便不加也是可以的)
> `mount -v -t ext3/ext4 /dev/<xxx> $LFS`
> `mount -v -t ext3 /dev/sda2 $LFS`
> `mount /dev/sda2 $LFS`
* (非必要)挂载并使用swap分区
> `/sbin/swapon -v /dev/<zzz>`

**相关实例与指令具体说明:**
* 这里与以后的说明都将/dev/sda2分区称为LFS分区，即目标系统根目录
* 交换分区(swap)的作用是可以有效的解决编译过程中所需内存的不足，所以可以分出一个小型磁盘分区来当作swap空间
* 所以swap的容量可以按需分配，而sda2当然是越大越好
* 宿主机(原主机)和LFS分区的swap是公用的，如果原宿主机拥有swap，就没有必要再新建一个了
* 有关于磁盘分区的标志与其它分区表类型和启动引导类型的内容这里就不做过多赘述了

---

**1.2.2 创建必要目录以及目录权限分配**

* 今后在第二阶段(临时系统)制作的时候会将所有的软件编译到`$LFS/tools`中，以便与第三阶段时所编译的软件完全分离
* 在目标系统成型后，便可将其遗弃
* 执行以下操作需要root权限
* 创建工具链目录`$LFS/tools` 
> `mkdir -v $LFS/tools`

* 在原主机内创建符号链接，用以指向LFS分区中新建的目录(/tools)
* 此时所创建的符号链接将永远指向`/tools`文件夹
> 即编译器，汇编器，链接器无论是在临时系统或是目标系统中都可以进行使用
* 配置符号链接
> `ln -sv $LFS/tools /`

**1.2.3 创建源代码编译用目录**
> `mkdir -v $LFS/sources`
* 权限分配
> `chmod -v a+wt $LFS/sources`

---

**1.2.4 添加LFS用户(自定义非特权用户命名)**
* 因为以root用户登陆时，一个操作失误便可以摧毁整个操作系统，所以在此需要新建一个非特权用户来对软件包进行编译
* 同时也是为了建立一个干净的工作环境，这里创建一个名为lfs的新用于作为新组(同样命名为lfs)的成员
* 添加新用户:
> `groupadd lfs`
* 将新用户lfs的shell设为默认bash，并将用户lfs添加到lfs组中，同时为lfs用户创建主目录
* 并对用户输入位置设置为空设备(null)，以防止可能从框架目录复制文件的情况
> `useradd -s /bin/bash -g lfs -m -k /dev/null lfs `
* 设置lfs用户密码，可以为空
> `passwd lfs`
* 将目录所有者改变为lfs
> `chown -v lfs $LFS/tools`
* 同时为用户lfs赋予访问$LFS/tools目录的所有权限
> `chown -v lfs $LFS/sources`
* 以lfs身份登陆主机
* 切换用户并启动shell环境
> `su - lfs`

---

**1.2.5 设置环境**

* 通过为bash shell创建两个开机启动文件，来设置合适的工作环境
* 以lfs用户的身份来创建一个新的`.bash_profile`文件
```
cat > ~/.bash_profile << "EOF" 
exec env -i HOME=$HOME TERM=$TERM PS1='\u:\w\$ ' /bin/bash 
EOF
```

**具体说明:**
* 当以lfs用户身份登录时，初始shell通常是一个login的shell
1. 它先读取宿主机的`/etc/profile`文件(很可能包括一些设定和环境变量)
2. 然后是`.bash_profile`文件
3. `.bash_profile`中的命令`exec env -i.../bin/bash`用一个除了HOME，TERM和PS1变量外
4. 其他环境完全为空的新shell代替运行中的shell
5. 这能确保不会有潜在的和意想不到的危险环境变量，从宿主机泄露到构建环境中
6. 这样做主要是为了确保环境的干净

---

**1.2.6 配置`.bashrc`文件**
* 新的shell实例是一个`non-login`的shell
* 它不会读取`/etc/profile`或者`.bash_profile`文件，而是读取`.bashrc`
* 创建`.bashrc`文件:
```
cat > ~/.bashrc << "EOF" 
set +h 
umask 022 
LFS=/mnt/lfs 
LC_ALL=POSIX 
LFS_TGT=$(uname -m)-lfs-linux-gnu 
PATH=/tools/bin:/bin:/usr/bin 
export LFS LC_ALL LFS_TGT PATH 
EOF
```

**具体说明:**
* `set +h`命令关闭了bash的哈希功能
* 设置用户文件新建时的掩码(umask)为 022，以确保新建的文件和目录只有其所有者可写，但任何人都可读可执行
* LFS 变量应设置成选定的挂载点
* `LC_ALL变量`控制某些程序的本地化，使它们的消息遵循特定国家的惯例
* 设置`LC_ALL`为`POSIX`或`C`(两者是等价的)，以确保在chroot环境中一切能如期望的那样进行
* `LFS_TGT变量`设置了一个虽非默认，但在构建交叉编译器、连接器和交叉编译临时工作链时，用得上到的兼容的机器说明
* 通过把`/tools/bin`放在标准`PATH变量`的前面，使得所有在临时主机中安装的程序，一经安装shell便能马上使用
* 与之配合的关闭哈希功能，能在临时主机环境中的程序在可用的情况下，限制使用宿主机中旧程序的风险 

---

* 1.2.7 启用配置
* 最后，启用刚才创建的用户配置
* 为构建临时工具完全准备好环境:
> `source ~/.bash_profile`

---



