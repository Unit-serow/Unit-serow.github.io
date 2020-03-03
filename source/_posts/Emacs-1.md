---
title: GNU Emacs-1
date: 2020-02-21 07:04:29
tags: [随笔,GNU/Linux]
categories: [软件,GNU] 
---

## Emacs-1

### Emacs快捷键快速参考(参考资料整理)

**基本快捷键(常用且泛用):**

* C/M/De说明:
> C(Control/Ctrl)
> M(Meta/Alt|Esc)
> De(Backspace)

|指令|作用|摘要|
|:----|:----|:----|
|C-x C-s|保存文件|保存|
|C-x C-w|使用其他文件名另存为文件|另存为|
|C-x C-f|"find"文件, 即在缓冲区打开/新建一个文件|新建|
|C-z|挂起emacs|挂起|
|C-x C-c|关闭emacs|关闭|
|C-x i|在当前光标处插入文件|插入|
|C-x C-v|关闭当前缓冲区文件并打开新文件|关闭缓冲区|
|C-x b|新建/切换缓冲区|新建缓冲区|
|C-x C-b|显示缓冲区列表|缓冲区信息|
|C-x k|关闭当前缓冲区|关闭缓冲区|
|M-n|重复执行后一个命令n次|宏|
|C-d|删除(delete)后一个字符|删除字符|
|M-d|删除后一个单词|删除字符串|
|C-k|移除(kill)一行|删除行|
|C-g|停止当前运行/输入的命令|停止|
|C-x u|撤销前一个命令|撤销|
|C-s|向后搜索|搜索|
|C-r|向前搜索|搜索|
|M-x shell|打开shell模式|shell|

---

**帮助指令:**

|指令|作用|
|:----|:----|
|C-h c|显示快捷键绑定的命令|
|C-h k|显示快捷键绑定的命令和它的作用|
|C-h l|显示最后100个键入的内容|
|C-h w|显示命令被绑定到哪些快捷键上|
|C-h f|显示函数的功能|
|C-h v|显示变量的含义和值|
|C-h b|显示当前缓冲区所有可用的快捷键|
|C-h t|打开emacs教程|
|C-h i|打开info阅读器|
|C-h C-f|显示emacs FAQ|
|C-h p|显示本机Elisp包的信息|

---

### 其它:

**指令集类型一共可以分为七种类型(具体可参考参考资料):**

1. 基本快捷键(Basic)
2. 光标移动基本快捷键(Basic Movement)
3. 编辑(Editint)
4. 重要快捷键(Important)
5. 在线帮助(Online-Help)
6. 搜索/替换(Seach/Replace)
7. 使用正则表达式(Regular expression)搜索/替换
8. 窗口命令(Window Commands)
9. 书签命令(Bookmark commands)
10. Text
11. Telnet
12. DIRectory EDitor (dired)
13. Shell
14. 宏命令(Macro-commands)
15. 编程(Programming)
16. GDB(调试器)
17. 版本控制(Version Control)

---

### 参考资料:

* 官方网站[跳转](https://www.gnu.org/software/emacs/emacs.html)
> `https://www.gnu.org/software/emacs/emacs.html`

* 官方手册[跳转](https://www.gnu.org/software/emacs/manual/html_mono/emacs.html)
> `https://www.gnu.org/software/emacs/manual/html_mono/emacs.html`

* Emacs Lisp[跳转](https://www.gnu.org/software/emacs/manual/html_mono/elisp.html)
> `https://www.gnu.org/software/emacs/manual/html_mono/elisp.html`

* 获取地址:[跳转](https://www.gnu.org/software/emacs/download.html#gnu-linux)
> `https://www.gnu.org/software/emacs/download.html#gnu-linux`

* 国内社区[跳转](https://emacs-china.org/)
> `https://emacs-china.org/`

* apt-get获取
> `apt-get -y install emacs`
> 插件和拓展的配置与安装本章节不会多做赘述

* spacemacs仓库/获取地址[跳转](https://github.com/syl20bnr/spacemacs)
> `https://github.com/syl20bnr/spacemacs`

* spacemacs获取方式
> `git clone https://github.com/syl20bnr/spacemacs ~/.emacs.d`

---

**其它指令参考网站:**

* CN-2015-Emacs常用基本快捷键[跳转](https://gist.github.com/shijinkui/2048195)
> `https://gist.github.com/shijinkui/2048195`

* CN-2008-Emacs快捷键列表[跳转](https://aifreedom.com/technology/112)
> `https://aifreedom.com/technology/112`
> 这个相当详细

* CN-2019-Emacs常用快捷键一览[跳转](https://qiutedyuan.github.io/blog/2019/06/12/Emacs%E5%B8%B8%E7%94%A8%E5%BF%AB%E6%8D%B7%E9%94%AE%E4%B8%80%E8%A7%88/)
> `https://qiutedyuan.github.io/blog/2019/06/12/Emacs%E5%B8%B8%E7%94%A8%E5%BF%AB%E6%8D%B7%E9%94%AE%E4%B8%80%E8%A7%88/`

---

[https://www.baidu.com/](https://www.baidu.com/)

[https://www.google.com/](https://www.google.com/)

---

## 补充内容

* 2020-02-21
> 20.46

---

### Spacemacs

**spacemacs参考资料**

* 其它功能拓展与插件

* 代码补全
> 自动补全 (company mode)
* 语法高亮
> 语法高亮 (Org-mode)
* 其它工具
> major mode
> minor mode 
* 编程/编译环境

* 在已经可以确定安装完成emacs之后，从Github仓库拉取spacemacs拓展
> `git clone --recursive https://github.com/syl20bnr/spacemacs ~/.emacs.d`

---

**参考文献:**

* 中文社区[跳转](https://emacs-china.org/c/spacemacs)
> `https://emacs-china.org/c/spacemacs`

* EN-文档[跳转](https://github.com/syl20bnr/spacemacs/blob/master/doc/DOCUMENTATION.org)
> `https://github.com/syl20bnr/spacemacs/blob/master/doc/DOCUMENTATION.org`

* 代码仓库[跳转](https://github.com/syl20bnr/spacemacs)
```
https://github.com/syl20bnr/spacemacs
https://github.com/syl20bnr/spacemacs.git
```

---

* EN-Wiki[跳转](https://en.wikipedia.org/wiki/Spacemacs)
> `https://en.wikipedia.org/wiki/Spacemacs`

* 技术博客子龙山人
> `https://zilongshanren.com/`

* CSND某博客[跳转](https://blog.csdn.net/csfreebird/article/details/52744771)
> `https://blog.csdn.net/csfreebird/article/details/52744771`

---

**可参考资源补充:**

* EN-手册地址[跳转](https://github.com/syl20bnr/spacemacs#linux-distros)
> `https://github.com/syl20bnr/spacemacs#linux-distros`

* CSDN-使用`.emacs.d`目录管理Emacs配置文件[跳转](https://blog.csdn.net/gxp/article/details/6970464)
> `https://blog.csdn.net/gxp/article/details/6970464`

* 某个人博客[跳转](https://bitmingw.com/2017/03/02/spacemacs-install-configuration/)
> `https://bitmingw.com/2017/03/02/spacemacs-install-configuration/`

---

### 相关工具整理:

* zsh
> Z shell(Zsh)是一款可用作交互式登录的shell及脚本编写的命令解释器
> Zsh对Bourne shell做出了大量改进，同时加入了Bash、ksh及tcsh的某些功能
> 实现工具: `oh-my-zsh`

* 参考网站:[跳转](https://www.jianshu.com/p/d194d29e488c)
> `https://www.jianshu.com/p/d194d29e488c`

* Python管理工具
> pyenv
> pyenv virtualenv

* 其它工具
> nvm
> npm

---

### 补充内容(spacemacs)-1: 

**spacemacs基本操作简述**

* spacemacs只是一份emacs的配置文件
* 通常只需要把克隆来的spacemacs放到`~/`目录下就可以直接启动与初始化了

* 以下为emacs匹配不到spacemacs的配置文件的解决方法:

* 先将原`~/.emacs.d`文件进行备份与移动，将由Git工具克隆来的文件下载到`~/`目录下(当前用户的根目录，默认非root)
* 再指定emacs启动文件的用户所有权(这里将emacs的启动文件的执行权交给了root)
> `chown root:root emcas.d`

* 启动emacs编辑器时，加载指定用户的初始化文件(这里用root用户来初始化emcas启动文件)
> `emacs -u root`

* 其它基本说明:
> 更新emacs配置，并重新加载emacs(.emacs.d)配置文件
> 备份并移动`~/.emacs`文件，并且拥有`~/.emacs.d`的执行所有权
> `~/.emacs.d/init.el`为emacs的启动脚本，任何关于emacs的配置都在这里进行
> `~/.emacs`为启动文件
> `~/.emacs.d`为启动配置文件
> 现在通常只有下者了

* 还有其它的解决办法
> 初始化emacs程序(将其卸载并重新安装)
> 保证emacs第一次启动的启动脚本的配置是spacemacs应该也可以

---

**相关资料归纳:**

* CN-Spacemacs 使用总结[跳转](https://scarletsky.github.io/2016/01/22/spacemacs-usage/)
> `https://scarletsky.github.io/2016/01/22/spacemacs-usage/`

* CN-Emacs学习(1)[跳转](https://www.jianshu.com/p/a7b8d1659b9b)
> `https://www.jianshu.com/p/a7b8d1659b9b`

* CN-15分钟学会Emacs Lisp (v0.2a)[跳转](https://learnxinyminutes.com/docs/zh-cn/elisp-cn/)
> `https://learnxinyminutes.com/docs/zh-cn/elisp-cn/`

* EN-Learn X in Y minutes(x分钟速成y技术)[跳转](https://learnxinyminutes.com/)
> `https://learnxinyminutes.com/`

* CN-Spacemacs入门与基本用法[跳转](https://ifun.dev/post/spacemacs_usage/)
> `https://ifun.dev/post/spacemacs_usage/`

* CN-emacs指令说明[跳转](https://wangchujiang.com/linux-command/c/emacs.html)
> `https://wangchujiang.com/linux-command/c/emacs.html`

---

**spacemacs基本配置**

* 配置Magit，用于辅助并集成Git进行远端版本管理

* EditorConfig
> 维护工具
> 让不同的编译器和IDE都按照相同的格式来格式化代码

* org-mode
> 代码自动补全

---

**相关参考(URL归纳目录):**

* CN-emacs自动补全[跳转](https://blog.csdn.net/hengrjgc/article/details/43231327)
> `https://blog.csdn.net/hengrjgc/article/details/43231327`

* CN-Spacemacs 与 Org-mode 配置与使用技巧[跳转](https://www.douban.com/note/706407786/)
> `https://www.douban.com/note/706407786/`

* CN-spacemacs 与 org-mode 配置与使用技巧 [跳转](http://mpwang.github.io/2019/02/06/productivity/)
> `http://mpwang.github.io/2019/02/06/productivity/`

* CN-十个高效的spacemacs配置[跳转](http://www.mamicode.com/info-detail-636363.html)
> `http://www.mamicode.com/info-detail-636363.html`

* CN-Spacemacs 使用总结[跳转](https://scarletsky.github.io/2016/01/22/spacemacs-usage/)
> `https://scarletsky.github.io/2016/01/22/spacemacs-usage/`

* spacemacs 中文教程[跳转](http://www.voidcn.com/search/bopuqg)
> `http://www.voidcn.com/search/bopuqg`

* 官方文档[跳转](https://github.com/syl20bnr/spacemacs/blob/master/doc/DOCUMENTATION.org)
> `https://github.com/syl20bnr/spacemacs/blob/master/doc/DOCUMENTATION.org`

* Vim User[跳转](https://github.com/syl20bnr/spacemacs/blob/master/doc/DOCUMENTATION.org)
> `https://github.com/syl20bnr/spacemacs/blob/master/doc/VIMUSERS.org`

---

### 补充内容(Spacemacs)-2

**spacemacs配置相关:**

* 在`~/.spacemacs`中的`dotspacemacs-additional-packages`内添加所需配置以使spacemacs支持所选服务

* Layer
> spacemacs为依赖与拓展的管理提供了独有layer(分层)机制
> 使其已被配置且各个不同类别的插件在保证独立性的同时还大幅的简化了对插件或拓展的管理与操作难度
> Layer基于Lisp编写与配置

* Package
> 是spacemacs默认的独立包管理器`SPC-T-s`启用package

* Evil
> 它能够为spacemacs提供vim的操作格式，为默认选项

---

**可用URL参考:**

* CN-Spacemacs 的配置[跳转](https://www.cnblogs.com/yangwen0228/p/10193245.html)
> `https://www.cnblogs.com/yangwen0228/p/10193245.html`

* CN-视频参考[跳转](https://youtu.be/MBrU-Py3HaA?list=PL-61yFRAEMlUMOtAeoYErz2yLe9IeTKRS)
> `https://youtu.be/MBrU-Py3HaA?list=PL-61yFRAEMlUMOtAeoYErz2yLe9IeTKRS`

* CN-Spacemacs使用中的FAQ[跳转](https://www.jianshu.com/p/354896569a90)
> `https://www.jianshu.com/p/354896569a90`

* CN-某博客Spacemacs[跳转](https://wayslog.com/2017/06/30/spacemacs/)
> `https://wayslog.com/2017/06/30/spacemacs/`

* CN-spacemacs配置自己的layers[跳转](https://www.jianshu.com/p/bdd64fecddce)
> `https://www.jianshu.com/p/bdd64fecddce`

---

**关键字:**

* layer
* package
* Evil

---

### 补充内容(Spacemacs)-3

**自动补全功能实现:**

* Org-mode
> Org-模式(Org-mode)是文本编辑软件Emacs的一种支持内容分级显示的编辑模式
> 这种模式支持写`to-do`列表，日志管理，做笔记，做工程计划或者写网页
> 意思就是大体作用类似于markdown
> 参考自: https://www.cnblogs.com/qlwy/archive/2012/06/15/2551034.html#sec-1
> 参考自: https://baike.baidu.com/item/org-mode/3339684?fr=aladdin

* spacemacs安装与配置[跳转](https://baike.baidu.com/item/org-mode/3339684?fr=aladdin)
> `http://www.fidding.me/article/12`

---

**Emacs/Spacemacs自动补全**

* 最基本需要用到以下插件(layer)中的自动补全支持
* 在`dotspacemacs-configuration-layers`里面新增所需layer
> auto-complete 自动弹窗
> yasnippet 自动补全
> popup 自动弹窗
> company 自动补全
> lsp-mode 自动补全
> Django 自动补全
> anaconda-mode(python)自动补全
* 这里的例子就举这么多，实际上数不胜数

---

* 配置文件
> auto-complete.el
> popup.el

---

**可用URL参考目录:**

* emacs 自动补全[跳转](https://blog.csdn.net/promanz/article/details/89384129?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task)
> `https://blog.csdn.net/promanz/article/details/89384129?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task`

* Emacs-107-开启全局自动补全模式[跳转](https://blog.csdn.net/grey_csdn/article/details/79477169?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task)
> `https://blog.csdn.net/grey_csdn/article/details/79477169?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task`

* Emacs基本配置，自动补全[跳转](https://blog.csdn.net/hengrjgc/article/details/43231327?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task)
> `https://blog.csdn.net/hengrjgc/article/details/43231327?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task`

* emacs代码补全插件介绍[跳转](https://blog.csdn.net/topgun_chenlingyun/article/details/9447755?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task)
> `https://blog.csdn.net/topgun_chenlingyun/article/details/9447755?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task`

* EMACS下弹出窗口式的Auto-Complete自动补全工具简单介绍[跳转](https://blog.csdn.net/hahazhouzhiqin/article/details/9735347)
> `https://blog.csdn.net/hahazhouzhiqin/article/details/9735347`

* Emacs-015-自动补全插件company的安装与使用[跳转](https://blog.csdn.net/grey_csdn/article/details/78966457)
> `https://blog.csdn.net/grey_csdn/article/details/78966457`

* spacemacs安装与配置[跳转](http://www.fidding.me/article/12)
> `http://www.fidding.me/article/12`

---

## spacemacs配置简述

* 从网络上下载的扩展包被放置于`~/.emacs.d/elpa`文件夹下
* `~/.spacemacs`为spacemacs配置文件

**配置文件内常见(常用)参数简述:**

* `dotspacemacs-configuration-layers`是启用的layer列表
* 初始列举的layer大多被双引号注释掉了，注释符号为`;;`
* 其中的themes-megapack用于下载各类皮肤，dotspacemacs-themes用于设置皮肤
* `dotspacemacs-editing-style`是默认编辑模式
* `evil mode`默认的对应值为`'vim`
* `dotspacemacs-maximized-at-startup`在启动时自动最大化窗口，可以将值设为`t`以开启此功能
* `dotspacemacs-line-numbers`设置是否显示行号，`nil`隐藏，`t`显示
* `dotspacemacs-whitespace-cleanup`删除多余的空白，推荐设置为'trailing`
* `spacemacs`的灵魂:`auto-completion`(自动完成)和`heml`
* `dotspacemacs-additional-packages'(web-mode)添加`web-mode`，同时也是在`dotspacemacs-additional-packages`里面添加包的基本格式
* `dotspacemacs-elpa-https nil`用于https检测，可设为`nil`

---

**可自定义选项参考:**
* user-init()选项内修改自定义配置
* (add-hook 'after-init-hook 'global-company-mode) 激活自动补全

* 默认配置
```
(setq-default

   dotspacemacs-themes '(monokai);;设置主题

   dotspacemacs-fullscreen-use-non-native t   ;;设置最大化不占用系统导航栏
   dotspacemacs-maximized-at-startup t   ;;设置窗口启动最大化
   dotspacemacs-line-numbers t   ;;开启行号
   dotspacemacs-auto-resume-layouts t ;;重启后自动打开关闭前alyout

)
```

---

* 参考自: https://bitmingw.github.io/2017/03/02/spacemacs-install-configuration/
* 皮肤网站: https://themegallery.robdor.com/

---



