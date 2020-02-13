---
title: Docker-Machine
date: 2020-02-08 18:23:23
tags: Docker
categories: [软件,虚拟化]
---

### Docker Machine

**概述:**
* 可以实现在虚拟主机上安装Docker
* 并且可以使用`docker-machine`命令来管理主机
* `Docker Machine`管理的虚拟主机可以是机上的，也可以是云供应商的
* 使用`docker-machine`命令，可以用于启动，检查，停止和重新启动托管主机，也可以升级Docker客户端和守护程序
* 以及配置Docker客户端与本地主机进行通信
* 用于实现使用本地主机便可以操控远端的镜像容器集群

**逻辑简述:**
[Client docker-machine[Client docker CLI[REST APT]]]-docker-machine create->[REST API[Server docker daemon]]

---

**基于Linux安装Docker Machine**
```
$ base=https://github.com/docker/machine/releases/download/v0.16.0 &&
  curl -L $base/docker-machine-$(uname -s)-$(uname -m) >/tmp/docker-machine &&
  sudo mv /tmp/docker-machine /usr/local/bin/docker-machine &&
  chmod +x /usr/local/bin/docker-machine
```

* 查看版本以验证是否安装成功
```
$ docker-machine version
docker-machine version 0.16.0, build 9371605
```

---

**对于machine version的使用**

1. 列出可用的机器
> `$ docker-machine ls`

2. 创建机器
* 创建一个名为serow的机器
> `$ docker-machine create --driver virtualbox serow`
* 参数`--driver`用于指定用来创建机器的驱动类型，这里是`virtualbox`

3. 查看机器的 ip
> `$ docker-machine ip serow`

4. 停止机器
> `$ docker-machine stop serow`

5. 启动机器*
> `$ docker-machine start serow`

6. 进入机器*
> `$ docker-machine ssh serow`

---

**docker-machine 命令参数明细**

|命令|作用|
|:----|:----|
|docker-machine active|用于查看当前激活状态的Docker主机|
|config|查看当前激活状态Docker主机的连接信息|
|creat|创建Docker主机|
|env|显示连接到某个主机需要的环境变量|
|inspect|以`json`格式输出指定Docker的详细信息|
|ip|获取指定 Docker 主机的地址|
|kill|直接杀死指定的 Docker主机|
|ls|列出所有的管理主机|
|provision|重新配置指定主机|
|regenerate-certs|为某个主机重新生成TLS信息|
|restart|重启指定的主机|
|rm|删除某台Docker主机，对应的虚拟机也会被删除|
|ssh|通过SSH连接到主机上，执行命令|
|scp|在Docker主机之间以及Docker主机和本地主机之间通过`scp`远程复制数据|
|mount|使用SSHFS从计算机装载或卸载目录|
|start|启动一个指定的Docker主机，如果对象是个虚拟机，该虚拟机将被启动|
|status|获取指定Docker主机的状态(包括:`Running`,`Paused`,`Saved`,`Stopped`,`Stopping`,`Starting`,`Error`)等|
|stop|停止一个指定的Docker主机|
|upgrade|将一个指定主机的Docker版本更新为最新|
|url|获取指定Docker主机的监听URL|
|version|显示 Docker Machine 的版本或者主机Docker版本|
|help|显示帮助信息|

