---
title: hexo博客文件远端备份与恢复
date: 2020-02-03 20:47:37
tags: [hexo]
categories: [软件]
---

### hexo博客文件远端备份与恢复

* 其实就是将本地工作区的数据上传到远端仓库
* 因为再创建一个代码仓库有点浪费，所以用再原仓库内建立新分支的方法去备份博客
* 在创建新分支之前先确保博客内有默认主分支master

**按顺序执行以下指令:**
* `git init  //创建一个新的Git仓库或初始化一个现有的仓库`
该命令创建一个空的Git版本库和暂存区，基本上具有对象库，指针(HEAD)库和模板文件等等的隐藏目录.git
现有存储库中运行git init命令是安全的，所以不会覆盖已经存在的数据
* `git add . `
将本地文件依次添加到暂存区
* `git commit -m 'hexo'(需要进行备份的文件名，比如说hexo的根目录)` 
将文件数据提交至本地暂存区文件内，然后再将暂存区的改动提交到本地的版本库
* `git branch hexo` 
创建一个名为hexo的新分支
* `git checkout hexo` 
切换到hexo分支上
* `git remote add origin Github仓库地址` 
让仓库地址/URL实现本地与远程Github仓库的对接
* `git push origin hexo(推送文件目录) `
推送本地工作区(仓库)内容到远程仓库的hexo分支，远程仓库的默认命名是origin

创建新的仓库时会默认建立.gitignore文件，用于将不需要备份的文件屏蔽

以后备份的时候只需要
```
git add .
git commit -m "Backname"
git push orgin hexo
hexo g与hexo d
```
---

**恢复博客**

在本地机器上克隆博客文件的hexo分支
`git clone https://github.com/yourgithubname/yourgithubname.github.io`

分别执行以恢复博客
```
npm install hexo-cli
npm install
npm install hexo-deployer-git
```
---

**其他指令**
```
git branch --set-upstream-to=origin/分支名称 //在所选仓库内设置默认分支
git remote //查看所有远程仓库
gir remote rm origin //删除所关联的远程仓库地址
git remote add origin 新仓库地址 //添加新仓库地址
git push orign master //提交到新仓库中的默认分支
git submodule init //初始化本地配置文件
git submodule update //抓取所有数据并检出项目中列出的合适的提交
git rm --cached file //从暂存区删除文件，工作区不做出改变
git checkout . //重新指定本地分支，用暂存区全部或指定的文件替换工作区的文件
git pull 参数[options]  仓库名[repository]  分支名[refspec...] //从一个仓库或者本地的分支拉取并合并代码，相当于 git fetch 跟着一个 git merge FETCH_HEAD
```
