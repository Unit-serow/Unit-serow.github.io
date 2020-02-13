---
title: Docker-2
date: 2020-02-06 16:40:10
tags: Docker
categories: [软件,虚拟化]
---

### Docker Engine-Community install

**Debian Docker 安装**

* Docker Engine-Community 支持版本:
`Buster 10与Stretch 9 (stable) / Raspbian Stretch`
* Docker Engine-Community 支持架构:
`x86_64(或amd64)armhf，和 arm64`

> 选定主机的首次安装需要设置Docker仓库，用以从仓库安装和更新Docker，而Raspbian系统必须使用shell脚本安装

**设置仓库**

安装apt依赖包，以通过HTTPS来获取仓库
```
$ sudo apt-get install \
   apt-transport-https \
   ca-certificates \
   curl \
   gnupg2 \
   software-properties-common
```

**添加Docker的官方GPG密钥**
`$ curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -`

> 通过搜索指纹的最后八个字符，验证目前主机是否拥有带指纹的密匙
> 密匙:`9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88`
> 执行:`$ sudo apt-key fingerprint 0EBFCD88`

```
pub   4096R/0EBFCD88 2017-02-22
      Key fingerprint = 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid                  Docker Release (CE deb) <docker@docker.com>
sub   4096R/F273FCD8 2017-02-22
```

**设置稳定版仓库**
```
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
```

* `lsb_release -cs`子命令用于返回Debian发行版的名称
* Docker对未经测试和不受支持的Debian发行版不提供任何保证

---

**安装 Docker Engine-Community**

* 更新apt包索引
`$ sudo apt-get update`

* 安装最新版本的 Docker Engine-Community和containerd 
`$ sudo apt-get install docker-ce docker-ce-cli containerd.io`

* 安装指定版本的 Docker Engine-Community
* 列出仓库中的可用版本
`apt-cache madison docker-ce`
* 使用`docker-ce |`后所输出的字符串安装指定版本，然后执行:
`$ sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io`

**卸载主机上Docker的旧版本**
* Docker的旧版本被称为`docker`，`docker.io`或`docker-engine`
`$ sudo apt-get remove docker docker-engine docker.io containerd runc`

**帮助指令**
```
docker command --help
man docker
```

---

**docker 镜像配置**

* Docker官方提供的中国镜像库:`https://registry.docker-cn.com`
* 以添加Docker官方镜像库地址`https://registry.docker-cn.com`为例

* upstart系统
`$ emacs /etc/default/docker`
* 修改其中`DOCKER_OPTS`的配置
`DOCKER_OPTS="--registry-mirror=https://registry.docker-cn.com"`
* 重启服务
`$ sudo service docker restart`

* systemd系统
`emacs /etc/docker/daemon.json`
* 如果没有就创建，在文件内添加:
`{"registry-mirrors":["https://registry.docker-cn.com"]}`
* 重启服务
`$ sudo systemctl daemon-reload`
`$ sudo systemctl restart docker`

* 检查配置是否生效
`$ docker info`
```
Registry Mirrors:
   https://registry.docker-cn.com/
```

---

**参考资料:**

官方手册:[跳转](https://docs.docker.com/)
`https://docs.docker.com/`

官方安装手册:[跳转](https://docs.docker.com/install/linux/docker-ce/debian/)
`https://docs.docker.com/install/linux/docker-ce/debian/`


