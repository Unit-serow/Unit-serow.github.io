---
title: Docker Compose-1
date: 2020-02-07 16:47:40
tags: Docker
categories: [软件,虚拟化]
---

### Docker Compose

**概述:**

* Compose是用于定义和运行多容器Docker应用程序的工具
* 通过Compose，可以使用YML文件来配置应用程序需要的所有服务
* 最后通过使用一个命令，就可以从 YML 文件配置中创建并启动所有服务
* [YAML](https://yaml.org/)官方文档

---

**安装 Compose**

* Github地址:[跳转](https://github.com/docker/compose/releases)
> `https://github.com/docker/compose/releases`

* 下载源码包(二进制文件)
* Docker Compose当前的稳定版本：
> `$ sudo curl -L "https://github.com/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose`
* 其中的1.25.4为版本号，可用于指定版本
* 提权至可执行文件
> `$ sudo chmod +x /usr/local/bin/docker-compose`
* 设置环境变量的软链接
> `$ sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose`
* 查看版本，以测试是否安装成功
> `$ docker-compose --version`
* 对于Alpine/Linux发行版，需要安装依赖包:`py-pip`，`python-dev`，`libffi-dev`，`openssl-dev`，`gcc`，`libc-dev`，以及`make`

---

**使用**
* 对Compose进行使用大概可分为三个步骤:
> 使用Dockerfile定义应用程序的环境
> 使用`docker-compose.yml`文件定义构成应用程序的服务，使其可以在隔离环境中一起运行
> 最后，执行`docker-compose up`命令来启动并运行整个应用程序

