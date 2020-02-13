---
title: Docker-1.1
date: 2020-02-09 03:11:01
tags: Docker
categories: 软件
---

### 基本指令

* 查看已有镜像
> `docker images`
* 参数:仓库源/标签/ID/创建时间/空间
> `debian tag [镜像ID]` # 添加标签

* 查看仓库内所有镜像文件
> `docker search debian`

* 拉取仓库内默认版本的debian镜像`(debian:latest)`
> `docker pull debian`

* 查看所有已创建容器
> `docker ps -a`

* 用容器启动所选镜像
> `docker run -it  --name [自定义命名] debian /bin/bash`

---

* 启动，停止，重启所选容器
> `docker start/stop/restart [容器ID]`
> 参数:`·-i交互式操作`，`-t终端`，`-d后台运行`

---

* 删除操作
> `docker rmi debian`删除镜像
> `docker rm -f`删除容器
> `docker container prune`删除所有停止的容器
* 容器必须停止才能进行删除

---

* 进入后台后使用`docker attach`或`docker exec [容器ID]`进入该容器
* 前者暂时性，后者永久性
* 重新进入容器时还必须加入原来设置的启动参数
* 比如`/bin/bash和-it`

---

* 设置[service]端口映射与绑定IP
> `docker run -p [可选的IP绑定]:[映射端口]:[原端口]/(udp/tcp) [镜像名] [启动脚本]`
> 参数:`-P`是随机映射，`-p`是指定映射

* 查看端口绑定情况
> `docker port [服务名]`

---

### 容器网络

* 父子关系这里都称为上下层级关系，与阶级关系不同
* 上级容器可以看到下级容器的关系

* 建立容器网络
> `docker network create -d bridge/overlay(网络类型) [网络命名]
> `overlay`应用于`swarm`

* 后台运行一个命名为`test1`的容器并把它并入`test-net`内，并开启交互式终端系统
> `docker run -itd --name test1 --network test-net debian /bin/bash`

* 任何加入此网络的容器都会达成互联的状态

---

* 设定所有容器域名和DNS
```
$ vim /etc/docker/daemon.json
{"dns" : ["111.111.111.111","1.1.1.1"]}
```

* 查看是否生效
> `docker run -it rm debian cat etc/resolv.conf`

* 指定容器设置域名和DNS服务器
> `docker run -it --rm _hostname=HOSTNAME --dns=IP_ADDRESS --dns-search=DOMAIN(搜索域) debian`
* 没有指定`--dns`和`--dns-search`，Docker会默认用宿主主机上的`/etc/resolv.conf`来配置容器的DNS

---

* 登陆`docker hub`
> `docker login`

* 退出`docker hub`
> `docker logout`

* 上传镜像
> `docker tag 本地镜像名 username/远端镜像名`

---

* 随笔
> `Docker Engine` 引擎
> `REST API` 通用接口
> `Docker daemon` 守护进程

* 自用简易指令集
