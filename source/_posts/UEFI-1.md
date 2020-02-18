---
title: EFI/UEFI-1
date: 2020-02-19 00:54:10
tags: [随笔]
categories: [软件,固件]
---

### EFI/UEFI-1

**概述:**
* 统一可扩展固件接口(Unified Extensible Firmware Interface)
* 作为BIOS的替代方案被用来定义操作系统与系统固件之间的软件界面
* 可扩展固件接口负责加电自检(POST)，联系操作系统以及提供连接操作系统与硬件的接口
* UEFI的前身是Intel在1998年开始开发的Intel Boot Initiative，后来被重命名为可扩展固件接口(Extensible Firmware Interface，缩写EFI)
* Intel在2005年将其交由统一可扩展固件接口论坛(Unified EFI Forum)来推广与发展，为了凸显这一点，EFI也更名为UEFI(Unified EFI)
* 位置说明:操作系统<->可拓展接口(UEFI/BIOS)<->系统固件<-系统硬件
* 在EFI规范中，一种突破传统MBR磁盘分区结构限制的GUID磁盘分区系统(GPT)被引入

---

### UEFI与BIOS

**UEFI**

* UEFI用模块化，C语言风格的参数堆栈传递方式，动态链接的形式构建的系统
* 较BIOS而言更易于实现，容错和纠错特性更强，缩短了系统研发的时间
* 它可以运行于x86-64、IA32、IA64等架构上（在个人电脑上通常是x86-64平台），突破传统16位代码的寻址能力，达到处理器的最大寻址
* 它利用加载EFI驱动程序的形式，识别及操作硬件，不同于BIOS利用挂载实模式中断的方式增加硬件功能
* 另外UEFI在概念上非常类似于一个低阶的操作系统，并且具有操控所有硬件资源的能力
> 但EFI的缔造者们在第一版规范出台时就将EFI的能力限制于不足以威胁操作系统的统治地位
---
* UEFI系统下的驱动程序可以由EFI Byte Code(EBC)编写而成
> EFI Byte Code是一组专用于EFI驱动程序的虚拟机器语言，必须在EFI驱动程序运行环境(Driver Execution Environment，或DXE)下被解释运行
> 采用EBC编写的EFI驱动程序拥有向下兼容性，以便在安装不同处理内不需要重新编写EFI驱动，所以UEFI无需对系统升级带来的兼容性因素作考虑
* 基于EFI的驱动模型可以使UEFI系统接触到所有的硬件功能
> 比如在操作系统运行以前浏览万维网站，实现图形化、多语言的BIOS设置界面，或者无需运行操作系统即可在线更新BIOS
---
* UEFI固件区分架构，在UEFI引导模式下，通常只能运行特定架构的UEFI操作系统和特定架构的EFI应用程序(EBC程序除外)
> 比如，采用64位UEFI固件的PC，在UEFI引导模式下只能运行64位操作系统引导程序
> 而在Legacy引导模式(即BIOS兼容引导模式)下，通常不区分操作系统的比特数，既可以运行16位的操作系统(如DOS)
> 也可以运行32位或64位的操作系统，和BIOS一样
---
* 在众多的分区类型中，EFI系统分区可以被UEFI固件访问，可用于存放操作系统的引导程序、EFI应用程序和EFI驱动程序
* EFI系统分区采用FAT文件系统，容量较小，在Windows操作系统下，默认是隐藏的
* UEFI固件通过运行EFI系统分区中的引导程序引导操作系统

**BIOS**

* BIOS必须将一段类似于驱动程序的16位代码(如RAID卡的Option ROM)放置在固定的`0x000C0000`至`0x000DFFFF`之间存储区中
> 运行这段代码的初始化部分，它将挂载实模式下约定的中断向量向其他程序提供服务
> 由于这段存储空间有限(128KB)，BIOS对于所需放置的驱动程序代码大小超过空间大小的情况无能为力
* BIOS的硬件服务程序都以16位代码的形式存在，这就给运行于增强模式的操作系统访问其服务造成了困难
> 因此BIOS提供的服务在现实中只能提供给操作系统引导程序或MS-DOS类操作系统使用
* 部分采用EFI技术的BIOS并不支持EFI引导

---

### 统一可扩展固件接口(UEFI)的构成

* 一般认为UEFI由以下几个部分构成:
* Pre-EFI初始化模块
* EFI驱动程序执行环境
* EFI驱动程序
* 兼容性支持模块(CSM)
* EFI高层应用
* GUID磁盘分区表

---

**实现逻辑:**

* 在实现中，统一可扩展固件接口(UEFI)初始化模块和驱动执行环境通常被集成在一个只读存储器中
* Pre-EFI初始化程序在系统开机的时候最先得到执行，它负责最初的CPU，芯片组及存储器的初始化工作，紧接着加载EFI的驱动程序执行环境(DXE)
* 当DXE被加载运行时，系统便具有了枚举并加载其他EFI驱动程序的能力
* 在基于PCI架构的系统中，各PCI桥及PCI适配器的EFI驱动程序会被相继加载及初始化
* 同时，系统进而枚举并加载各桥接器及适配器后面的各种总线及设备的EFI驱动程序，以此周而复始，直到最后一个设备的EFI驱动程序被成功加载
> 正因如此，EFI驱动程序可以放置于系统的任何位置，只要能保证它可以按顺序被正确枚举

**例如:**

1. 有一个具PCI-E总线接口的RAID存储适配器，其EFI驱动程序一般会放置在这个设备的符合PCI规范的扩展只读存储器(PCI Expansion ROM)中
2. 当PCI总线驱动程序被加载完毕，并开始枚举其子设备时，这个存储适配器旋即被正确识别并加载它的EFI驱动程序
3. 部分EFI驱动程序还可以放置在某个磁盘的EFI系统分区(ESP)中，只要这些驱动程序不是用于加载这个磁盘的驱动的必要部件

---

**CSM**

* CSM是在x86平台UEFI系统中的一个特殊的模块
* 它将为不具备UEFI引导能力的操作系统(如Windows XP)以及16位的传统Option ROM(即非EFI的Option ROM)提供类似于传统BIOS的系统服务
* Secure Boot和CSM不兼容，因此在UEFI固件设置中打开CSM前，需要在UEFI固件设置中关闭Secure Boot

---

**采用UEFI固件的x86/x64系统类别**

* 类别0，这类系统使用x86 BIOS固件，只支持传统操作系统
* 类别1，这类系统采用支持UEFI和Pi规范的固件，激活CSM层功能，只支持传统操作系统
* 类别2，这类系统采用支持UEFI和Pi规范的固件，激活CSM层功能，同时支持传统和UEFI引导的操作系统
* 类别3，这类系统采用支持UEFI和Pi规范的固件，不再提供或完全关闭CSM层功能，只支持由UEFI引导的操作系统
* 类别3+，在类别3的系统基础上提供并激活Secure Boot功能

---

### 版本历史:

* 1.1版本于2002年12月发布(EFI)
* 2.1版本于2007年1月7日发布(UEFI)
> 增加与改进了加密编码(cryptography)
> 网络认证(network authentication)
> 用户接口架构(User Interface Architecture)
* 2.3版本于2009年5月9日发布
* 最新为2.7版本

* Linux内核自2000年开始，已经支持EFI引导
> 早期使用ELILO作为EFI下的引导程序
> 现在，GRUB的EFI版本已代替ELILO，大多数Linux发行版已使用GRUB作为UEFI下的引导程序
* VMware Workstation支持对UEFI的模拟
> 但是在VMware Workstation 11以前，VMware Workstation并未正式支持UEFI，需要手动编辑虚拟机的.vmx文件以打开虚拟机的UEFI

---

### Secure Boot相关

* 在UEFI 2.3.1 Errata C规范中定义了一项名为"Secure Boot"的协议
* Secure Boot只允许加载有适当数字签名的EFI驱动程序和EFI引导程序，以此Secure Boot可让引导过程更安全

* 自由软件基金会(FSF)的Josh Gay对UEFI的"Secure Boot"实现提出忧虑，并发表公开声明及连署说：
> 我们—连署者—敦促所有实现了UEFI中称为"Secure Boot"的电脑制造商立即允许自由的操作系统可以被安装
> 基于尊重用户的自由权以及确切保护用户安全，制造商必须允许电脑拥有者停用引导限制，或是提供一个确切可能的方法让他们安装并运行自由的操作系统
> 我们承诺我们将不会购买、也不会推荐剥夺用户重要自由的电脑
> 并且，我们将积极地敦促社会大众避免如此禁锢用户的系统

* 2012年1月，微软发布一份关于OEM硬件认证的文件
> 指出所有的x86和x86-64设备应该将UEFI Secure Boot引导
> 不过可以改用一个可让用户增加数字签名的自定义secure boot模式

* RHEL(从RHEL 7开始)，CentOS(从CentOS 7开始)，Debian(从Debian 10开始)等Linux发行版已经支持SecureBoot

---

**其他概念:**

* EFI
* UEFI
* BIOS
* RAID
* Option ROM
* CSM
* SecureBoot
* x86-64(AMD64和Intel 64)
* SMBIOS
* ACPI

---

**外部链接:**

* EN-统一可扩展固件接口论坛[跳转](https://uefi.org/)
> `https://uefi.org/`

* EN-FSF对于SecureBoot的评价[跳转](https://www.fsf.org/campaigns/secure-boot-vs-restricted-boot)
> `https://www.fsf.org/campaigns/secure-boot-vs-restricted-boot`

---
