---
title: vim-1
date: 2020-05-16 00:55:16
tags: 随笔
---

<center><strong>Vim-1</strong></center>

<!-- more -->

* Vim 有以下三种工作模式：

1. 命令模式（Command mode），进入时默认
2. 输入模式（Insert mode），i & a 唤醒
3. 底线命令模式（Last line mode），英文的冒号":"

* vim 默认的配置文件通常处于 `/etc/vim/vimrc` 目录内（debian系）
> 只不过还可以再`~`（主目录）下创建一个`.vimrc`文件，有如：`$ touch .vimrc`
> 配置文件的结束标志：call vundle#end()

* vim常用的插件管理器为Vundle，当然还有别的，比如[Vim-plug](https://linux.cn/article-9751-1.html)
>Vundle的仓库： `git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim`

* Vundle 当中常用的命令：
> 安装插件：`:BundleInstall`
> 更新插件：`:BundleUpdate`
> 清除不需要的插件：`:BundleClean`
> 列出当前的插件：`:BundleList`
> 搜索插件：`:BundleSearch`

---

* 可用参考资料：
> 代码补全（YouCompleteMe）、语法高亮、自动缩进、python补全（pydiction）

https://www.cnblogs.com/feiyuhuo/p/10274236.html
https://www.cnblogs.com/xuqiang/archive/2011/04/15/2016475.html
https://www.jianshu.com/p/1839f1fb3f08
https://blog.csdn.net/jiaolongdy/article/details/17889787?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase
https://blog.csdn.net/weixin_44408476/article/details/105082509
https://zhuanlan.zhihu.com/p/35626421
https://www.cnblogs.com/littlesuns/p/9845386.html
https://byvoid.com/zhs/blog/vim-syntex/
http://www.coozhi.com/youxishuma/g4/90585.html
https://blog.csdn.net/Fffhhas/article/details/88724615
https://blog.csdn.net/MK_chan/article/details/89047170
https://blog.csdn.net/qq_26877377/article/details/80717755?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-4.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-4.nonecase

---

https://www.jianshu.com/p/128ea159b587

---



