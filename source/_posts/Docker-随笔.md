---
title: Docker-随笔
date: 2020-02-09 17:05:25
tags: Docker
categories: 软件
---

### Docker 随笔

* Docker 由Go语言编写

* Docker 主要分支(三大项目)

1. Docker Engine-Community
> docker社区

2. Docker Compose
> docker自动化操作-YAML/Go

3. Docker Machine
> docker集群化管理

---

* 基本概念
* dockerfile
* 容器集群网络
* docker虚拟机
* swarm集群

---

* 绝对基本流程
```
docker images
docker search
docker pull
docker run
search ps -a
docker rmi
docker rm -f 
docker start/restart/stop
```
* 能直接拉就直接拉，不到极端情况下最好别总想着整一些类似于dockerfile的花活

---

* docker hub[跳转](https://hub.docker.com)
> `https://hub.docker.com`

* 文档[跳转](https://docs.docker.com/)
> `https://docs.docker.com/`

---

### 容器服务安装并启动实例

**容器-操作系统**
* Ubantu/Debian/CentOS
* 先`docker search`看一下镜像
* 直接`pull`过来然后`exec`就行
* 默认是最新版本`Ubantu/Debian/CentOS:latest`
* Docker Hub内点击`Sort by`选项卡查看其他版本
* 这里暂时不阐述通过Dockerfile构建的方法

1. Ubuntu 镜像库地址[跳转](https://hub.docker.com/_/ubuntu?tab=tags&page=1)
`https://hub.docker.com/_/ubuntu?tab=tags&page=1`

2. CentOS 镜像库地址[跳转](https://hub.docker.com/_/centos?tab=tags&page=1)
`https://hub.docker.com/_/centos?tab=tags&page=1`

3. Debian 镜像库地址[跳转](https://hub.docker.com/_/debian?tab=tags&page=1)
`https://hub.docker.com/_/debian?tab=tags&page=1`

---

**容器-web服务**
* Nginx/Apache/Node.js/Tomcat

1. Nginx
* 说明:Nginx是一个高性能的HTTP和反向代理web服务器，同时也提供了`IMAP/POP3/SMTP`服务
* 镜像库地址[跳转](https://hub.docker.com/_/nginx?tab=tags)
> `https://hub.docker.com/_/nginx?tab=tags`

* 运行容器:
> $ docker run --name nginx-test -p 8080:80 -d nginx
* 参数说明:
> `--name nginx-test`:容器名称
> `-p 8080:80`:端口进行映射，将本地8080端口映射到容器内部的80端口
> `-d nginx`:设置容器在在后台一直运行

---

2. Apache-httpd
* 镜像库地址[跳转](https://hub.docker.com/_/httpd?tab=tags)
> `https://hub.docker.com/_/httpd?tab=tags`

* 运行容器:
> `$ docker run -p 80:80 -v $PWD/www/:/usr/local/apache2/htdocs/ -v $PWD/conf/httpd.conf:/usr/local/apache2/conf/httpd.conf -v $PWD/logs/:/usr/local/apache2/logs/ -d httpd`
* 参数说明:
> `-p 80:80`:将容器的 80 端口映射到主机的 80 端口
> `-v $PWD/www/:/usr/local/apache2/htdocs/`:将主机中当前目录下的`www`目录挂载到容器的`/usr/local/apache2/htdocs/`
> `-v $PWD/conf/httpd.conf:/usr/local/apache2/conf/httpd.conf`:将主机中当前目录下的`conf/httpd.conf`文件挂载到容器的`/usr/local/apache2/conf/httpd.conf`
> `-v $PWD/logs/:/usr/local/apache2/logs/`:将主机中当前目录下的`logs`目录挂载到容器的`/usr/local/apache2/logs/`

---

3. Node.js
* 镜像库地址[跳转](https://hub.docker.com/_/node?tab=tags)
> `https://hub.docker.com/_/node?tab=tags`
* 运行容器:
> `docker run -itd --name node-test node`
* 进入容器内部查看其服务版本

---

4. Tomcat
* 镜像库地址[跳转](https://hub.docker.com/_/tomcat?tab=tags)
> `https://hub.docker.com/_/tomcat?tab=tags`
* 运行容器:
```
$ docker run --name tomcat -p 8080:8080 -v $PWD/test:/usr/local/tomcat/webapps/test -d tomcat
acb33fcb4beb8d7f1ebace6f50f5fc204b1dbe9d524881267aa715c61cf75320
```
* 参数说明:
> `-p 8080:8080`:将容器的8080端口映射到主机的8080端口
> `-v $PWD/test:/usr/local/tomcat/webapps/test`:将主机中当前目录下的`test`挂载到容器的`/test`

---

**容器-数据库**
* MySQL/MongoDB/Redis

* MySQL
* 镜像库地址[跳转](https://hub.docker.com/_/mysql?tab=tags)
> `https://hub.docker.com/_/mysql?tab=tags`

* 运行容器:
> `$ docker run -itd --name mysql-test -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql`
* 参数说明:
> `-p 3306:3306`:映射容器服务的3306端口到宿主机的3306端口，外部主机可以直接通过宿主机`ip:3306`访问到MySQL的服务
> `MYSQL_ROOT_PASSWORD=123456`:设置MySQL服务root用户的密码

---

* MongoDB
* 简介:`MongoDB`是一个免费的开源跨平台面向文档的`NoSQL`数据库程序
* 镜像库地址:[跳转](https://hub.docker.com/_/mongo?tab=tags&page=1)
> `https://hub.docker.com/_/mongo?tab=tags&page=1`
* 运行容器:
> `$ docker run -itd --name mongo -p 27017:27017 mongo --auth`
* 参数说明:
> `-p 27017:27017`:映射容器服务的27017端口到宿主机的27017端口，使外部可以直接通过宿主机`ip:27017`访问到`mongo`的服务
> `--auth`:需要密码才能访问容器服务
* 接着使用以下命令添加用户和设置密码，并且尝试连接
> `$ docker exec -it mongo mongo admin`
* 创建一个名为`admin`，密码为123456的用户
>  `db.createUser({ user:'admin',pwd:'123456',roles:[ { role:'userAdminAnyDatabase', db: 'admin'}]});`
* 尝试使用上面创建的用户信息进行连接
> `db.auth('admin', '123456')`

---

* Redis
* 简介:是一个开源的使用`ANSI C`语言编写、支持网络、可基于内存亦可持久化的日志型,`Key-Value`的`NoSQL`数据库，并提供多种语言的`API`
* 镜像库地址:[跳转](https://hub.docker.com/_/redis?tab=tags)
> `https://hub.docker.com/_/redis?tab=tags`
* 运行容器:
> `$ docker run -itd --name redis-test -p 6379:6379 redis`
* 通过`redis-cli`连接测试使用`redis`服务
> `$ docker exec -it redis-test /bin/bash`

---

* PHP[跳转](https://hub.docker.com/_/php?tab=tags)
> `https://hub.docker.com/_/php?tab=tags`

* Python[跳转](https://hub.docker.com/_/python?tab=tags)
> `https://hub.docker.com/_/python?tab=tags`

* redis.conf[跳转](https://github.com/antirez/redis/blob/unstable/redis.conf)
> `https://github.com/antirez/redis/blob/unstable/redis.conf`
