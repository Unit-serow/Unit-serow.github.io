---
title: Docker-3
date: 2020-02-06 18:44:34
tags: Docker
categories: [软件,虚拟化]
---

### Docker容器的基本命令与基本应用

**基本操作命令**

**拉取镜像**
`$ docker pull --help`
`$ docker pull [OPTIONS] NAME:[:TAG|@DIGEST]`
如果本地没有镜像，用pull从仓库里拉个镜像用
`$ docker pull debian`

**基于已有镜像启动容器服务**
`$ docker run --help`
`$ docker run [OPTIONS] IMAGE [COMMAND] [ARG...]`
`$ docker run -i -t debian /bin/bash`
* `参数-i`启动交互式选项，`参数-t`启动终端选项
* `debian`:也就是debian镜像
* `/bin/bash`:放在镜像后的是被执行指令，这里用`/bin/bash`来启动交互式`Shell`
* 退出当前容器内终端执行`exit`

---

**查看所有容器**
`$ docker ps -a`
* 查询最后一次创建的容器
`$ docker ps -l`
* 输出参数说明

|参数|说明|
|:----|:----|
|CONTAINER ID|容器ID|
|IMAGE|使用的镜像|
|COMMAND|启动容器时运行的命令|
|CREATED|容器的创建时间|
|STATUS|容器状态|
|NAMES|自动分配的容器名称|

* 其中状态有七种
> created:已创建
> restarting:重启中
> running:运行中
> removing:迁移中
> paused:暂停
> exited:停止
> dead:死亡
> PORTS:容器的端口信息和使用的连接类型(tcp\udp)

---

**启动一个已停止的容器**
`$ docker start [容器ID]`
* `参数-d`用于指定容器的运行模式，加了此参数的程序默认不会进入程序，进入容器需要使用指令`docker exec`
* 在后台内利用容器debian运行debian-test程序
* `$ docker run -i -t -d --name debian-test debian /bin/bash`

**停止容器**
`$ docker stop [容器 ID]`

**重启容器**
`$ docker restart [容器 ID]`

**进入容器**
`$ docker attach/exec --help`
* 在执行`参数-d`后，容器启动后会进入后台
* 此时想要进入容器，可以通过以下指令进入：
> docker attach
> docker exec(使用docker exec命令时退出容器终端，不会导致容器的停止)
`$ docker attach 容器ID`(如果从这个容器退出，会导致容器的停止)
`$ docker exec -i -t 容器ID /bin/bash`(从这个容器退出，不会导致容器的停止)

**导出本地的某个容器**
`$ docker export [容器ID] > [生成的文件名(可以是tar或其他压缩文件)]`
> 把指定ID的容器快照导入到本地文件，保存地址是现在所处目录

**导入容器快照**
`$ docker import --help`
`$ docker import [OPTIONS] file|URL|- [REPOSITORY[:TAG]]`
> 将快照文件`debian.tar`导入到镜像`image-file/debian:v1`内
`$ cat docket/debian.tar | docker import - image-test/debian:v1`
> 还可以通过指定URL或者某个目录来导入
`$ docker import http://example.com/exampleimage.tgz example/imagerepo`

**删除容器**
`$ docker rm -f [容器ID]`
* 清理所有已中止容器
`$ docker container prune`

---

**利用docker运行某个应用程序**

* 拉取某个应用程序
`$ docker pull [应用程序名]`
`$ docker run -d -P [被拉取的程序名] [运行脚本]` 
> `参数-d`让容器在后台运行
> `参数-P`将容器内部使用的网络端口映射到我们使用的主机上
> 如果程序占用了某一端口，`docker ps`的时候会显示占用端口以及映射信息(PORST)
* 通过`-p参数`来设置不一样的端口
`$ docker run -d -p [原端口:指定端口] [被拉取的程序名] [运行脚本]`

**查看应用程序或容器使用的端口以及映射情况**
`$ docker ps`
`$ docker port [容器ID/程序名]`

**查看应用程序日志**
`docker logs [容器ID/程序名]`
> 用于查看容器内部的标准输出
> `参数-f`用于让`docker logs`输出容器内部的标准输出，类似于Linux内的`tail -f`命令

**查看应用程序进程**
`$ docker top [容器ID/程序名]`

**检查应用程序底层信息**
`$ docker inspect [容器ID/程序名]`
> 会返回一个记录着关于选中应用程序的Docker容器配置和状态信息的文本

**停止应用程序所在容器**
`$ docker stop [容器ID/程序名]` 

**重启应用程序所在容器**
`$ docker start [容器ID/程序名]` 

**移除应用程序所在容器**
`$ docker rm [容器ID/程序名]`   
> 删除容器时，容器必须是停止状态

---

**帮助命令:**

* 直接执行`docker`，查看Docker客户端的所有可用指令选项
* docker command --help，查看所选命令的帮助文件
