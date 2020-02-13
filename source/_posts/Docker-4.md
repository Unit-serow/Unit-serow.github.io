---
title: Docker-4
date: 2020-02-06 21:17:20
tags:
---

### Docker-镜像，网络，连接以及仓库的使用

**Docker 容器镜像的使用**

* 管理和使用本地的docker镜像
* 查看本地主机已有镜像
> `$ docker images`
* 各参数说明:

|参数|说明|
|:----|:----|
|REPOSITORY|表示镜像的仓库源|
|TAG|镜像的标签|
|IMAGE ID|镜像ID|
|CREATED|镜像创建时间|
|SIZE|镜像大小|

* 同一仓库源可以有多个`TAG`，代表这个仓库源的不同个版本
* `REPOSITORY:TAG`用于定义不同的镜像
* 例如使用`debian`，如果不指定一个镜像的版本标签，Docker 将默认使用`debian:latest`镜像

**获取镜像**
* 执行命令拉取10.2.0版本的debian镜像
`$ docker pull debian:10.2.0`
> 获取之后可直接基于此镜像来运行容器
> 还可以从[Docker Hub](https://hub.docker.com/)上获取镜像
> `https://hub.docker.com/`

**搜索镜像**
* 执行命令搜索指定镜像名的镜像
> `$ docker search [镜像名]`
> 比如搜索一个httpd的镜像来用作web服务
> `$ docker search httpd`

* 各参数说明:
|参数|说明|
|:----|:----|
|NAME|镜像仓库源的名称|
|DESCRIPTION|镜像的描述|
|OFFICIAL|是否 docker 官方发布|
|stars|类似 Github 里面的star|
|AUTOMATED|是否支持自动构建|

> 然后直接拉取镜像
> `$ docker pull httpd`

**删除镜像**
* 执行以下命令:
> `$ docker rmi 镜像名`

---

**创建镜像/制作镜像**
* 当docker的镜像仓库中没有所需求的docker镜像时，可以制作镜像或对镜像进行修改再上传

**更新镜像**
* 从已经创建的容器中更新镜像，并且提交此镜像
> 更新镜像之前，基于所选镜像来创建一个容器
> `$ docker run -t -i debian:10.2.0 /bin/bash`
> 在容器内使用`apt-get update`命令来进行更新
> 操作完成之后，键入`exit`退出容器
* 使用`docker commit`来提交容器副本
`$ docker commit -m="has update" -a="name" [Containers ID] /debian:v2`
> `参数-m`用于指定提交的描述信息
> `参数-a`用于指定镜像作者
> `Containers ID`:容器 ID
> `debian:v2:`指定要创建的目标镜像名
* 最后`docker images`查看新镜像，并用其启动容器

**构建镜像**
* 使用命令`docker build`，创建一个新的镜像
* 创建名为`Dockerfile`的文件，其中包含的指令用来指示Docker如何构建所选镜像
* 编写完Dockerfile之后通过docker build命令来构建一个新的镜像
> `docker build -t [目标镜像名] [指定绝对路径]`
> `参数-t`用于指定要创建的目标镜像名
> `参数.`用于指定Dockerfile 文件所在目录，可以指定Dockerfile 的绝对路径

**设置镜像标签**
* `docker tag`命令，为镜像添加一个新的标签
> `docker tag [镜像ID] [用户名称/镜像源名(repository name)]:[新的标签名(tag)]`

---

**Docker 容器连接**

* 容器中可以运行一些网络应用，从实现而让任意机器可以通过网络端口访问运行在docker容器内部的服务
* 要实现让任意机器(内部与外部)可以访问这些应用，可以通过 -P 或 -p 参数来指定端口映射
* 还可以指定容器绑定的网络地址，比如绑定本地主机的`127.0.0.1`

**网络端口映射的管理**

> `docker run -d -P [网络服务名称] [服务的启动脚本]`
* 参数说明:
* 参数-P用于创建容器，此时该网络服务绑定本地主机的默认端口
* 参数-p用于指定容器端口所绑定的主机端口
* 具体区别
> 参数-P是让容器内部端口随机映射到主机的高端口
> 参数-p是让容器内部端口绑定到指定的主机端口

> `docker run -d -p [原端口:指定绑定端口] [应用程序名称] [程序的启动脚本]`
* 然后执行docker ps 就会发现服务已改变端口映射

**指定容器绑定的网络地址**
* 这里绑定127.0.0.1:
> `docker run -d -p [127.0.0.1:原端口:指定绑定端口] [应用程序名称] [程序的启动脚本]`
* 此时就可以通过绑定的IP地址，来访问容器被指定绑定的接口
* 默认都是绑定TCP端口，如果要绑定UDP端口，可以在端口后面加上`/udp`
* `docker port`命令可以让我们快捷地查看端口的绑定情况

---

### Docker 容器互连

* 端口映射不是唯一把Docker连接到另一个容器的方法
* Docker内有一个连接系统允许将多个容器进行连通，以此共享被连接容器的信息
* Docker连接会创建一个子父关系，其中父容器可以看到子容器的信息
* 先给容器进行统一的命名，以方便管理
> `docker run -d -P --name [自定义容器名] [应用程序名称] [程序的启动脚本]`
> `参数--name`用于定义容器名

**创建docker网络**
> `docker network create -d bridge [Containers-net]`
> `参数-d`用于指定Docker的网络类型，有`bridge`与`overlay`
> 其中`overlay`网络类型用于`Swarm mode`

**连接容器**
* 运行一个容器并连接到新建的`Containers-net`网络
> `$ docker run -itd --name test1 --network Containers-net debian /bin/bash`
* 打开新的终端，再运行一个容器并加入到 test-net 网络:
> `$ docker run -itd --name test2 --network Containers-net debian /bin/bash`
* 使用test1和test2两个容器互相ping一下以测试是否建立联系，如果没有ping命令就进行安装
> `apt install iputils-ping`
* 可以在一个容器里安装好之后把容器包装成镜像，再以新的镜像重新运行以上两个容器
* 如果有多个容器之间需要互相连接，可以使用`Docker Compose`

**配置容器DNS**

* `/etc/docker/daemon.json`文件中增加以下内容来设置全部容器的DNS:
```
{
  "dns" : [
    "111.111.111.111",
    "3.3.3.3"
  ]
}
```
* 设置后，启动容器的DNS会自动配置为`111.111.111.111 和 3.3.3.3`
* 配置完，需要重启Docker服务才能生效 
> `/etc/init.d/docker restart`
* 查看容器的DNS是否生效可以使用以下命令，它会输出容器的DNS信息:
> `$ docker run -it --rm debian  cat etc/resolv.conf`
* 只想在指定的容器设置 DNS，则可以使用以下命令
> `docker run -it --rm host_debian  --dns=111.111.111.111 --dns-search=test.com debian`

* 参数说明：
> 参数`-h HOSTNAME`或`--hostname=HOSTNAME:`设定容器的主机名，它会被写到容器内的`/etc/hostname`和`/etc/hosts`
> 参数`--dns=IP_ADDRESS:`添加DNS服务器到容器的`/etc/resolv.conf`中，让容器用这个服务器来解析所有不在`/etc/hosts`中的主机名
> 参数`--dns-search=DOMAIN:`设定容器的搜索域，当设定搜索域为`.example.com`时，在搜索一个名为`host`的主机时，DNS不仅搜索`host`，还会搜索`host.example.com`
> 如果在容器启动时没有指定`--dns`和`--dns-search`，Docker会默认用宿主主机上的`/etc/resolv.conf`来配置容器的DNS

---

**仓库管理**
* 仓库(Repository)用于集中存放镜像
* 目前Docker官方维护了一个公共仓库Docker Hub
* 大部分需求都可以通过在Docker Hub中直接下载镜像来实现
* 网址为`https://hub.docker.com`，[跳转](https://hub.docker.com)
* 使用之前需要注册账户

* 登陆Docker hub执行
> `$ docker login`
* 退出 docker hub执行
> `$ docker logout`
* 查找镜像
> `$ docker search [镜像名]`
* 拉取镜像
> `$ docker pull [镜像名]`

**推送镜像**
* 把本地的镜像推送到Docker Hub
* `username`为Docker账号的用户名
> `$ docker tag [镜像名]:[版本] [username/镜像名:版本]`
> `$ docker image ls`
> `$ docker push [username/镜像名:版本]`
* 最后查看一下
> `$ docker search [username/镜像名]`

---

**参考资料**

官方文档:[跳转](https://docs.docker.com/)
`https://docs.docker.com/`

