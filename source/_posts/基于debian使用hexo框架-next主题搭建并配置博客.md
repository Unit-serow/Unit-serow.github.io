---
title: 基于debian使用hexo框架-next主题搭建并配置博客
date: 2020-01-28 23:18:46
tags: hexo
categories: 软件
---

### 对于debian的基本配置与hexo的安装

apt源的设置与一些基本软件的配置和准备这里就不过多阐述了
先修改一下/etc/hosts内的所配置IP,保证机器能ping通github.com
`vim /etc/hosts` 内添加 `192.30.253.113 github.com`

接下来安装hexo所依赖的几个程序：npm，git，node.js
`apt-get install npm*`
`apt-get install git*`
`apt-get install node.js*`
安装完之后检查一下版本或者whereis一下看看所否健在
最后再安装hexo软件
`npm install -g hexo-cli`
安装完--version检查一下版本

---

### hexo的基本操作

hexo --help
[官方中文文档与手册](https://hexo.io/zh-cn/docs/index.html)
hexo安装完毕后可以先进行一下测试
于任意目录下新建一个文件夹 `mkdir blog`
进入文件夹后分别执行`hexo init,hexo g,hexo s`
然后使用浏览器访问<u>localhost:4000</u>查看所否成功 

---

### hexo链接github库

利用npm安装hexo部署程序/插件
`npm install --save hexo-deployer-git`
`vim /*/blog/_config.yml`
修改最下方的#deployment配置
```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: https://github.com/你所建立的仓库地址
  branch: master
```
执行`hexo d`开始远程部署，其中需要用户输入仓库所在帐号的帐号和密码

---

### hexo修改主题

这里推荐两个个人感觉生态最好的两个hexo主题-next与yilia
进入blog目录下直接执行克隆命令
`git clone https://github.com/iissnan/hexo-theme-next themes/next`
或
`git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia`
此时的主题文件被存储于/blog/theme目录下
`cd _condig.yml`
修改#extensions中的theme，将原主题landscape修改为next或yilia

---

### hexo安装搜索插件与RSS插件

添加并配置RSS
`npm install hexo-generator-feed --save`
修改hexo配置文件为
```
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
        plugins:
                hexo-generator-feed
                #Feed Atom
        feed:
                type: atom
                path: atom.xml
                limit: 20
```
对主题文件添加：
```
feed:
        type: rss2
        path: rss2.xml
        limit: 5
        hub:
                content: 'true'
```

添加并配置search-搜索
`npm install hexo-generator-searchdb --save`
修改hexo配置文件为
```
# 搜索
  search:
          path: search.xml
          field: post
          format: html
          limit: 10000
```
修改主题配置文件为
找到local search，然后把enable设置为true

其余类似于菜单，头像，链接与装饰的配置可以[参考官方文档](http://theme-next.iissnan.com/)

---

### 关于文章的书写格式与基本要求

hexo文章书写的语法都来自于Markdown
Markdown所一种可以使用普通文本编辑器编写的标记语言
目的是通过简单的语法来让普通文本的内容具有一定的格式
详情参考: [Markdown中文文档](https://markdown-zh.readthedocs.io/en/latest)

---



