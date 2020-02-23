---
title: Debian GNU/Linux-2
date: 2020-02-23 01:36:50
tags: [随笔,GNU/Linux]
categories: [软件,GNU]
---

## Debian GNU/Linux-2

* 网络配置问题统一解决方案

### Debian网络配置基本命令

* 输出网卡与网络配置情况
> `ip -a/ifconfig`

* 查看所有已有网卡
> `networkctl`

* 网卡配置目录
> /etc/network/interfaces

**网卡配置说明:**

* 配置静态IP地址
```
auto eth0 		#开机自动激活
iface eth0 inte static 	#静态IP
address IP 		#本机IP
netmask 255.255.255.0 	#子网掩码
# network IP
# broadcast IP
gateway IP		#路由网关
```

* DHCP自动获取(动态IP地址)
```
auto eth0
iface eth0 inet dhcp
```

* 配置好之后保存配置，重启网卡(多种方式)
> `service networking restart`	#service工具
> `systemctl restart network`	#systemctl工具
> `/etc/init.d/network-manager restart`
> `/etc/init.d/networking restart`

* 重启指定网卡
> `ifdown eth0`
> `ifup eth0`

* 配置DNS
> `vi /etc/resolv.conf`
> `nameserver 0.0.0.0`

---

### 名称与各参数简述与解释:

**eth(ethernet)**
> 有线网卡
> 物理网卡
> 如:eth0，eth1，eth2...则代表网卡一，网卡二，网卡三...
> 还可称为en
---
* eth各接口说明
> eth0=lan接口
> eth1=wan接口
> br-lan=lan网桥
> br-lan 虚拟设备，用于LAN口设备桥接，可以用`brctl show`查看使用情况
---
* en(ethernet)标识说明:
> o:主板板载网卡，集成是的设备索引号
> p:独立网卡，PCI网卡
> s:热插拔网卡，USB之类的扩展槽索引号
> nnn(数字):MAC地址+主板信息计算得出唯一序列
---
**lo**
> 代表localhost，即127.0.0.1
> 虚拟设备，自身的回环网设备
---
**ens**
> ens33为自动备援模式，名称定为ens33
> eno1表示主板BIOS内置的网卡
> ens1表示主板BIOS中内置的PCI-E网卡
> enp2s0为PCI-E独立网卡
> eth0:如果没有使用以上任何一个，则将返回默认的网卡名
---
* wlan
> 无线网卡
> wlan0=无限端口
---

**网络接口的传统命名方式(可预测命名方案)**
**传统命名:**
* 以太网:ethX,[0,oo)
> 例如eth0，eth1...
* PPP网络:pppX, [0,...]
> 例如，ppp0, ppp1, ...

---

### NONA

1. 设置网卡
```
nano /etc/network/interfaces  /etc/network/interfacesbak   	#备份原有配置文件
nano /etc/network/interfaces   			#编辑网网卡配置文件
auto lo
auto eth0  					#开机自动连接网络
iface lo inet loopback
allow-hotplug eth0
iface eth0 inet static   				#static表示使用固定ip，dhcp表述使用动态ip
address 192.168.21.166   				#设置ip地址
netmask 255.255.255.0  				#设置子网掩码
gateway 192.168.21.2    				#设置网关
ctrl+o   						#保存配置
ctrl+x   						#退出
```

2. 设置DNS
```
cp  /etc/resolv.conf   /etc/resolv.confbak    	#备份原有dns配置文件
nano /etc/resolv.conf   			#编辑配置文件
nameserver 8.8.8.8   			#设置首选dns
nameserver 8.8.4.4   			#设置备用dns
ctrl+o   					#保存配置
ctrl+x   					#退出
```

---

### 相关概念

* 网络上关于以下概念的资料数不胜数，这里就不再多做阐述了

**OSI七层模型:**
> 由上至下简述(程序至底层)
> 应用层/表示层/会话层/传输层/网络层/数据链路层/物理层
> 上层依赖于下层，下层为上层提供服务
> OSI内的每一层模型都有属于自己的协议集与功能集
> 层与层之间相互独立且相互依赖

* 中文维基[跳转](https://zh.wikipedia.org/wiki/OSI%E6%A8%A1%E5%9E%8B)
> `https://zh.wikipedia.org/wiki/OSI%E6%A8%A1%E5%9E%8B`

* TCP/IP
> IP:互联网协议
> TCP:传输控制协议
> 三次握手与四次握手
> 任何基于互联网协议蔟与协议套组都基于TCP/IP

* HTTP
> 超文本传输协议
> 无状态协议
> 大部分实现都是基于TCP的

* DNS
> 域名系统

* 其它常用协议
> 应用层:BGP/DHCP/HTTPS/IMAP/NNTP/NTP/POP/SMTP/SNMP/SSH/Telnet等等
> 传输层:UDP/TLS/SSL/DCCP等等
> 网络层:IP/ICMP/IGMP/IPsec等等
> 链接层:APR/PPP/DSL/ISDN等等

---

### 操作流程(逻辑)整合/简述

1. 查看网络配置
2. 查看已有网卡
3. 启动或重启网卡
4. 设置配置文件(静态IP或动态IP)
5. 配置网关
6. 配置DNS
7. 保存配置并重启网卡

* 任何网络与本地的流量与数据的传输都需要经过本地或无限的网卡
* 流量与数据的抓取也只是读取经由网卡的信息并进行输出
* 配置无线或有限网的前提是所处的物理环境已有网络支持
* 网卡用于联网的虚拟信息处理方式，网络离不开物理层面的支持
* 网卡被归纳为设备内

---

**参考资料:**

* Linux系统运维[跳转](https://www.osyunwei.com/)
> `https://www.osyunwei.com/`

---


