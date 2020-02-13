---
title: Docker Machine/Swarm-1.1
date: 2020-02-09 14:38:25
tags: Docker
categories: 软件
---

### docker machine-基本命令

* 虚拟机与容器的区别:虚拟机内可以定义容器

* 列出已有虚拟机
> `docker-machine ls`

* 创建虚拟机
> `docker-machine create --driver [virtualbox] [test]`
> 参数--driver用于指定虚拟机驱动类型,这里是virtualbox

* 虚拟机驱动一览[跳转](https://docs.docker.com/machine/drivers/)
> `https://docs.docker.com/machine/drivers/`

* 查看虚拟器的ip
> `docker-machine ip [test]`

---

* 管理命令
> `docker-machine start/restart/stop test`

* 帮助与检阅命令
> `version/help/info`

* 官方文档[跳转](https://docs.docker.com/machine/reference/create/)
> `https://docs.docker.com/machine/reference/create/`

---

**指令摘要**

|命令|作用|
|:----|:----|
|kill|杀死指定主机|
|rm|删除指定主机|
|ssh|连接主机|
|upgrade|更新|
|url|获取监听url|
|scp|复制|
|regenerate-certs|刷新TLS|

---

* 工作节点(worker node)
* 管理节点(manager node)

* 在VMware里安装虚拟机的虚拟机驱动时需要
* 点开虚拟机设置里的处理器选项卡
* 勾选虚拟化引擎选项卡

---

### Docker Swarm集群-基本命令

* 创建管理节点(manager node)
> `docker-machine create -d virtualbox swarm-manager`
* 连入机器后执行
> `docker swarm init --advertise-addr [创建机器时分配的 ip]`
* 然后拷贝输出指令

* 创建工作节点(worker node)
* 进入工作节点运行拷贝的指令将其设置为工作节点

---

* 随机部署服务到集群中
* `alpine`是操作系统
> `docker service create --replicas 1 --name 服务名 alpine ping docker.com`

* 查看部署情况
> `docker service ps [服务名]`

* 查看具体信息
> `docker service inspect --pretty [服务名]`

* 扩展服务到多节点(两个)
> `docker service scale [服务名=2]`

* 删除服务
> `docker service rm [服务名]`

* 查看所有节点
> `docker node ls`

* 关闭服务节点
> `docker node update --availability drain swarm-worker1`

* 开启服务节点
> `docker node update --availability active swarm-worker1`

* `Active/Drain`分别代表开启与关闭

---

**滚动升级**
* 前提是已存在指定服务
* 创建服务
> `docker service create --replicas 1 --name redis --update-delay 10s redis:3.0.6`

* 滚动更新
> `docker service update --image [服务名:版本号] [指定已有的服务镜像]`









