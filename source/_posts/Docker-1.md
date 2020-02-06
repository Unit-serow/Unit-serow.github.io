---
title: Docker-1
date: 2020-02-06 14:42:25
tags: Docker
categories: [软件,虚拟化]
---

### Docker的基本概述与原理简述

**概述:**
* 基于google公司退出的Go语言实现
* 基于apache2.0协议，项目代码在github上进行维护
* Docker项目的目标是实现轻量级的操作系统虚拟化解决方案
* Docker的基础是linux容器(LXC)等技术，Docker在LXC[^1]的基础上Docter进行了进一步的封装，让用户不需要去关心容器的管理，从而使其操作更为简便
[^1]: LXC，其名称来自Linux软件容器（Linux Containers）的缩写，一种操作系统层虚拟化（Operating system–level virtualization）技术，为Linux内核容器功能的一个用户空间接口，关于LXC更详细的内容这里先不做阐述

**docker和传统虚拟化方式的不同之处**
* 可见容器技术Docker是在操作系统层面上实现虚拟化，直接对本机的操作系统进行复用
* 而传统方式则是在硬件层面上实现虚拟化
* 引用自官方文档:
>传统的(virtual machines)虚拟化技术不仅需要包含应用程序本身和必要的依赖所需要的存储空间以及容量，还需要承受若干个完整的操作系统所占有的存储空间，这些操作系统所占有的存储空间往往以GB为单位
>Docker容器引擎只包含了其应用程序以及依赖项，它在主机操作系统的用户空间内作为一个完全被隔离且独立的进程去运行，同时与其他容器共享内核，所以说它不仅拥有VM内资源隔离和分配技术所带来的优点，还拥有更强的可移植性和效率等优势

**Docker与传统虚拟化方式相比，所拥有的优势**
* 拥有更快速的交付和部署
Docker允许开发者在装有应用和服务本地容器做开发，从而直接集成到可持续开发流程中，以在整个开发周期中都可以完美的辅助开发者实现快速交付
* 高效的部署和扩容
因docker容器引擎的高可移植性，使其可以在任何软硬件平台上运行
这种可兼容的移植性可以让开发者把任何应用程序从一个硬件平台上直接迁移到另外一个硬件平台上
Docker的可兼容移植性和轻量特性可以很轻松的实现负载的动态管理，使开发者可以快速扩容或方便的下线某一应用和服务，这种速度将趋近实时
* 更高的资源利用率
Docker 对系统资源的利用率很高，一台主机上可以同时运行数千个 Docker 容器。容器除了运行其中应用外，基本不消耗额外的系统资源，使得应用的性能很高，同时系统的开销尽量小
以传统虚拟机的方式运行10个不同的应用就要起10个虚拟机，而Docker 只需要启动10个相互隔离的应用即可
* 更简单的管理
使用 Docker，只需要简易的修改，就可以替代以往大量的更新工作
所有的修改都以增量的方式被分发和更新，从而实现自动化并且高效的管理

---

**Docker引擎简述**
* Docker引擎是一个C/S结构的程序
* 简要流程:
* `(contiainer-manages/image-manages/network-manages/network-manages)->client docker CLI`
* `client docker CLI->REST API->server doceker deamon`
* Server是一个常驻进程
* REST API 实现了client和server间的交互协议
* CLI 实现容器和镜像的管理，为用户提供统一的操作界面

**Docker架构简述**
* Docker使用C/S架构
* 客户端，Docker程序与主机程序镜像由接口通信
* 指令由客户端发出，而Docker内部的镜像由主机经由接口提供
* 任何指令对镜像的操作都在Docker程序内部的独立化容器服务内完成

**逻辑简述**
* 最初由client发出管理指令
* 经由`DOCKER_HOST`接口操作docker daemon(程序)内的容器以及程序镜像(包括操作系统)
* docker deamon中已存在其注册表内的程序由`DOCKER_HOST`接口返回给docker deamon内作为镜像使用
* 而程序及系统的镜像再被分布给docker deamon内部的独立容器服务所管理
* 简而言之就是命令最后被传输到所指定镜像的容器服务内，进入其容器，对其程序进行操作
* 简要流程:
* `Client(指令)-DOCKER_HOST->Docker deamon<-DOCKER_HOST-Registry(注册表内已有程序)`
* `Docker->Images(Rigistry)->Containers`
* `从而实现Client->Containers`

---

**关于Docker最基本的核心概念**

* 镜像(Image)
Docker镜像(Image)，镜像其实就是一个只读的模板文件
例如：一个镜像可以包含一个完整的操作系统环境，里面仅安装了Apache或用户需要的其它应用程序
镜像可以用来创建 Docker 容器，一个镜像可以创建很多容器
Docker 提供了一个很简单的机制来创建镜像或者更新现有的镜像，用户可以直接从其他人那里下载一个已经做好的镜像来直接使用
镜像(Image)就是一堆只读层(read-only layer)的统一视角
这些只读层堆叠在一起，除了最下面的只读层，其它的只读层都会由指针指向它所对应的下一层
这些层是Docker内部的实现细节，并且能够在docker宿主机统一的的文件系统[^2]上访问到
[^2]: 统一文件系统(Union File System)技术能够将不同的层整合成一个文件系统，为这些层提供了一个统一的视角，这样就隐藏了多层的存在，在用户的角度看来，只存在一个文件系统


简要结构流程:
```
read-only layer:
Images(union file system):
read-only layer-(指针)->read-only layer-(指针)->read-only layer-(指针)->read-only layer->...
```

```
read-write layer:
Images(union file system):
bash/process->RW union file system
read-write layer-(指针)->read-only layer-(指针)->read-only layer-(指针)->read-only layer->...
```

* 仓库(repository)
仓库(Repository)是集中存放镜像文件的目录
仓库和仓库注册服务器(Registry)的区别不大
仓库注册服务器上通常存放着多个仓库，每个仓库中又包含了多个镜像，每个镜像有不同的标签(tag)
仓库分为公开仓库(Public)和私有仓库(Private)两种形式，最大的公开仓库是Docker Hub，存放了数量庞大的镜像供用户下载
国内公开的镜像仓库有很多，在我设置的友情连接里有几个我常用的镜像源的地址
用户也可以在本地网络内创建一个私有仓库
当用户创建了自己的镜像之后就可以使用 push 命令将它上传到公有或者私有仓库，这样下次在另外一台机器上使用这个镜像时候，只需要从仓库上 pull 下来就可以了
Docker 仓库的概念跟 Git 类似，注册服务器可以理解为 GitHub 这样的托管服务平台

* 容器(container)
Docker 利用容器(Container)来运行应用，容器是从镜像创建的运行实例
它可以被启动、开始、停止、删除，每个容器都是相互隔离的、保证安全的平台
容器的定义和镜像近乎相同，也是一堆层的统一视角，唯一区别在于容器的最上面那一层是可读可写的
一个运行态容器被定义为一个可读写的统一文件系统加上隔离的进程空间和包含其中的进程
所以说一个容器中的进程可以对文件进行修改、删除、创建，这些改变都将作用于可读写层

* Docker 客户端(Client)
Docker 客户端通过命令行或者其他工具与Docker的守护进程通信
[Docker SDK](https://docs.docker.com/develop/sdk/) 
`https://docs.docker.com/develop/sdk/`

* Docker 主机(Host)
一个物理或者虚拟的机器用于执行Docker守护进程和容器

---

**参考文献与获取方式**

官网[跳转](https://www.docker.com/)
`https://www.docker.com/`

文档[跳转](https://docs.docker.com/)
`https://docs.docker.com/`

docker中国区镜像源
`https://registry.docker-cn.com`

获取[跳转](https://docs.docker.com/get-docker/)
`https://docs.docker.com/get-docker/`

获取Docker Engine-Debian[跳转](https://hub.docker.com/editions/community/docker-ce-server-debian)
`https://hub.docker.com/editions/community/docker-ce-server-debian`



