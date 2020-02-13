---
title: Docker Swarm-集群
date: 2020-02-09 13:47:40
tags: Docker
categories: [软件,虚拟化]
---

### Swarm 集群管理

**概述:**

* `Docker Swarm`是Docker的集群管理工具
* 它将`Docker主机池`转变为单个虚拟Docker主机
* `Docker Swarm`提供了标准的`Docker API`
* 目的是使所有任何已经与Docker守护程序通信的工具都可以使用Swarm轻松地扩展到多个主机

* 支持的工具包括但不限于以下各项：
* Dokku
* Docker Compose
* Docker Machine
* Jenkins

**原理概述:**
* `swarm集群`由管理节点(manager)和工作节点(work node)构成
* `swarm mananger`:负责整个集群的管理工作包括集群配置,服务管理等所有跟集群有关的工作
* `work node`:即为`available node`,主要负责运行相应的服务来执行任务(task)
* 逻辑简述
* 管理节点(swarm manager)内存储着若干个服务(service)的副本(replicas)文件
* 工作节点(available/worker node)内存储这服务的标识与服务的镜像文件(container)
* 管理节点将所有的服务副本都分配到工作节点内，并管理与控制工作节点内的任务执行
> [swarm manager[service replicas]]->[available node[task[container(service:latest)]]]
> swarm manager->available node-1/available node-2/available node-3/available node-N

---

**应用**
* 以`Docker Machine`与`virtualbox`进行实践，需要先确保主机已安装`virtualbox`

* 创建docker机器:
> `$ docker-machine create -d virtualbox swarm-manager`

---

* 创建管理节点(manager node)
* 初始化`swarm`集群，进行初始化的这台机器，就是集群的管理节点
> `$ docker-machine ssh swarm-manager`
> `$ docker swarm init --advertise-addr 192.168.99.101`
> `--advertise-addr`后的IP为创建机器时分配的ip

* 当为机器分配IP之后，命令行会输出向集群内添加工作节点的指令(连接令牌)
> `To add a worker to this swarm，runthe following command`
> `docker swarm join --token [...]`

---

* 创建工作节点(worker node)
* 复制上面输出的指令(会被自动截断)
> `$ docker swarm join --token [...]`
> 输出`The node joined a swarm as a worker`

---

* 查看集群信息
> `docker info`
> 输出内容中`Swarm active`内的`managers`与`node`即为节点信息

---

* 部署服务器到集群中
* 跟集群管理有关的任何操作，都是在管理节点上操作的

* 随机指派任一工作节点，并于工作节点上创建任意的一个服务
> `docker@swarm-manager:~$ docker service create --replicas 1 --name [service name] alpine ping docker.com`

* 查看服务部署情况:
> `docker@swarm-manager:~$ docker service ps [service name]`

* 查看`service`部署的具体信息:
> `docker@swarm-manager:~$ docker service inspect --pretty [service name]`

---

* 扩展集群服务

* 将service服务扩展到若干个节点
> `docker@swarm-manager:~$ docker service scale [service name]=[节点数]`
* 查看服务部署情况:
> `docker@swarm-manager:~$ docker service ps [service name]`

---

* 删除服务
> `docker@swarm-manager:~$ docker service rm [service name]`
* 查看服务部署情况:
> `docker@swarm-manager:~$ docker service ps [service name]`

---

* 滚动升级服务
* 将redis旧版本通过滚动升级至更高版本
* 创建一个3.0.6版本的redis
> `docker@swarm-manager:~$ docker service create --replicas 1 --name redis --update-delay 10s redis:3.0.6`
* 滚动升级redis
> `docker@swarm-manager:~$ docker service update --image redis:3.0.7 redis`
* 查看redis服务部署情况:
> `docker@swarm-manager:~$ docker service ps redis`

---

* 停止某个节点接收新的任务
* 查看所有的节点：
> `docker@swarm-manager:~$ docker node ls`

* 默认所有的节点都是`Active`, 可以接收新的任务分配
* 停止节点`swarm-worker1`:
> `docker node update --availability drain swarm-worker1`
* 此时`swarm-worker1`状态变为`Drain`
* 不会影响到集群的服务，只是`swarm-worker1`节点不再接收新的任务
* 会使集群的负载能力有所下降

* 重新激活节点指令:
> `docker@swarm-manager:~$  docker node update --availability active swarm-worker1`

---

**参考资料**

* 虚拟机驱动[跳转](https://docs.docker.com/machine/drivers/)
> `https://docs.docker.com/machine/drivers/`

* 官方文档[跳转](https://docs.docker.com/machine/reference/create/)
> `https://docs.docker.com/machine/reference/create/`

---

**其他资源**

* Docker官方主页[跳转](https://www.docker.com)
> `https://www.docker.com`

* Docker官方博客[跳转](https://blog.docker.com/)
> `https://blog.docker.com/`

* Docker官方文档[跳转](https://docs.docker.com/)
> `https://docs.docker.com/`

* Docker Store[跳转](https://store.docker.com)
> `https://store.docker.com`

* Docker Cloud[跳转](https://cloud.docker.com)
> `https://cloud.docker.com`

* Docker Hub[跳转](https://hub.docker.com)
> `https://hub.docker.com`

* Docker的源代码仓库[跳转](https://github.com/moby/moby)
> `https://github.com/moby/moby`

* Docker发布版本历史[跳转](https://docs.docker.com/release-notes/)
> `https://docs.docker.com/release-notes/`

* Docker常见问题[跳转](https://docs.docker.com/engine/faq/)
> `https://docs.docker.com/engine/faq/`

* Docker远端应用 API[跳转](https://docs.docker.com/develop/sdk/)
> `https://docs.docker.com/develop/sdk/`

---

**Docker国内镜像源**

* 阿里云[跳转](https://help.aliyun.com/document_detail/60750.html)
> `https://help.aliyun.com/document_detail/60750.html`

* 网易云加速器
> `http://hub-mirror.c.163.com`

* 中国官方加速器
> `https://registry.docker-cn.com`

* ustc的镜像
> `https://docker.mirrors.ustc.edu.cn`

* daocloud
> `https://www.daocloud.io/mirror#accelerator-doc`(注册后使用)
