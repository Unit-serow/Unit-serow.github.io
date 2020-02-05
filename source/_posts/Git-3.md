---
title: 分布式版本控制系统-Git-2
date: 2020-02-04 14:13:34
tags: 2.应用与拓展
categories: [软件,Git]
---

### 分布式版本控制系统(Distributed Version Control) Git-第二章节

**基本操作**
* 上篇文章的末尾写了一点关于git创建新仓库和克隆项目的基本操作
* 这一章着重对暂存区内快照的管理与操作和分支的管理与操作进行说明
* 在`git init`后，在工作区的根目录会生成`.git`子目录，它就是本地主机的Git仓库，所有关于工作区项目的快照数据都存放在此目录下
* Git主要工作就是创建和保存工作区中项目的快照及与其他时间段的快照进行对比

1. `git add`
用于将工作区修改或进行操作的任何文件添加到缓存目录，也就是暂存区
`git add .`
添加当前项目的所有文件

2. `git status`
用于查看工作区当前的状态，执行完`git status`就能看到工作区向暂存区进行的任何操作
可以添加参数，比如添加`-s参数`，以输出经过简化的结果
`A/M filename`的意思是这个文件在添加到暂存区之后又有改动了

3. `git diff`
用以查看执行git status 输出结果的详细信息
参数信息
* `git diff`命令会输出暂存区以修改但尚未写入暂存区的改动的区别
* `git diff`尚未写入暂存区的改动
* `git diff --cached`查看已写如暂存区的改动
* `git diff HEAD`查看已写入暂存区的与未写入暂存区的所有改动
* `git diff --stat`输出简明的diff结果

4. `git commit`
将暂存区的内容添加到仓库中
因为每一次提交都要输入一次github的用户名和邮箱地址，所以可以先配置一下用户名和邮箱地址
```
git config --global user.name '用户名'
git config --global user.email 邮箱地址
```
`参数-m`在命令行中提供提交注释，如果没有此参数，Git就会自动打开一个编辑器以填写提交信息
`参数-a`可以跳过`git add`提交至暂存区

5. `git reset HEAD filename`
`filename`是指已提交到暂存区的内容
用于取消已缓存的内容
执行`git reset HEAD`以取消之前的`git add`，并且不包含下一个提交完成后的暂存区快照

6. `git rm`
从工作区删除某个文件，需要从已跟踪文件的清单中移除，然后再去提交
`git rm filename`
如果该文件修改过并且已经提交到暂存区而还要删除的话，必须使用强制删除`参数-f`
`git rm -f filename`
把文件从暂存区删除，或者说是从跟踪清单中删除，使用`--cached`参数
`git rm --cached filename`
使用`-r`参数用以递归删除，删除该目录下的所有文件和子目录
`git rm -r`文件目录

7. `git mv`
用于移动或重命名一个文件夹，目录或软链接
`git mv filename newfilename`

8. `git push` 
用于将本地工作区的最新消息推送到远端仓库

9. `git pull`
用于从远端仓库拉取最新的版本到本地工作区，并且自动与工作区内部的项目与数据自动合并(merge)

10. `git fetch`
用于是从远端仓库拉取最新版本到本地工作区，并且不会自动合并

11. `git merge`
用于从指定的分支合并到当前的分支，从而合并两个分支
`git pull`相当于`git fetch + git merge`
---

**Git查看提交日志**
12. `git log`
* `参数--oneline`查看简明版本
* `参数--graph`查看分支，合并等操作的日志，并显示拓扑图
* `参数--reverse`逆向输入所有日志
* `参数--author=用户名`查看指定用户的提交日志
* `参数--since，--before，--after，--until`查看指定日期
日志命令参考[跳转](https://git-scm.com/docs/git-log)
`https://git-scm.com/docs/git-log`

13. git 标签
`git tag -a 标签名`
用于给当前快照打上标签
---

**使用Git连接远端的Github仓库**

添加一个新的远程仓库
14. `git remote add shortname url`

查看当前的远程库
15. `git remote`

拉取远程库
从远程仓库克隆新分支与数据
16. `git fetch alias`
然后执行git merge 将远程分支到本地工作区所在的分支
17. `git merge alias/branch`
从远端仓库提取更新数据并尝试合并到当前分支
一般执行完`git fetch`之后就会紧接着执行`git merge`，前者去对数据进行过滤，获取当前工作区没有的新数据，后者用于将新数据合并到本地工作区当前分支的项目

推送到远程仓库
18. `git push alias branch`
将本地(branch)分支中的暂存区文件推到(alias)远端仓库上的(branch)分支
用于将本地暂存区的新数据推到某个远端仓库

删除远端仓库
19. `git remote rm [别名]`


**生成ssh key**
20. * `ssh-keygen -t rsa -C "youremail@example.com"`
* 会在`/root/.ssh`目录生成密匙文件，打开`id_rsa.pub`，复制里面的key
* 然后进入Github并登入Github，点击头像内的`setting`选项卡内的`SSH and GPG keys`中的`SSH Keys`选项卡
* 将文件里的key拷贝到key中，title随意，然后`add ssh key`
* 验证是否成功
```
ssh -T git@github.com
Hi Unit-serow! You've successfully authenticated, but GitHub does not provide shell access.
```
具体可以参考一下[跳转](https://help.github.com/articles/generating-ssh-keys)
`https://help.github.com/articles/generating-ssh-keys`




