---
title: GNU Gettext
date: 2020-02-02 13:59:34
tags: [1.认识与概述,GNU/Linux]
categories: [软件,GNU]
---

### GNU Gettext 第一章节

**GNU 国际化(i18n)库**

**概述:**

* 国际化与本地化函数库
* GNU gettext是GNU translation project中最重要的一步 
* GNU通用性翻译计划
* 这个项目的达成将会让GNU拥有更大的经济与用户结构，从而拥有更多的资本

**引用自官方文档:**

> 在以前，通常GNU内部或大量其它的自由软件中的程序源代码都是拿英文编写或记录的，并且在与用户交互的界面所使用的也是英语
> 当世界上所有的开发人员之间使用一种通用的语言去交流会让开发的过程变得极为方便
> 但是，在全世界范围内的大多数人对于英文的理解能力和学习深度远不如母语，所以它们更愿意使用母语进行日常工作
> 并且大多数人只是希望让屏幕上其它晦涩难懂的语言少一点，而自己的母语多一点
> 所以就有了GNU Gettext
> 该软件包为程序员，翻译人员与用户提供了一套完善的工具和文档集
> 更准确的说，gnu gettext所使用的程序是一组工具，提供了一个框架来帮助其他GNU软件包生成多语言的消息

**这个工具包括了以下的一组程序:**
* 一套如何编写程序，从而让消息目录支持的规则
* 一套如何为目录本身和文件命名的规则
* 一个运行时库，用于支持检索翻译后的消息
* 一些独立程序，以各种方式处理可翻译的字符串或已翻译字符串的集合

GNU Emacs拥有实现这套程序的插件或拓展，感兴趣的可以去查询有关GNU Emacs的消息

---

逻辑简述:
以下内容参考自:[跳转](https://www.gnu.org/software/gettext/manual/html_node/Program-Index.html#Program-Index)
`https://www.gnu.org/software/gettext/manual/html_node/Program-Index.html#Program-Index`
* xgettext程序从源代码生成.pot文件，作为源代码中序翻译内容的模板
* 而翻译者需要工作的对象是.po文件，它是有msginit程序从.pot模板文件生成的
* 翻译者用maginit初始化中文翻译文件时可以执行`msginit --locale=cn --input=name.pot`
* 然后编辑所生成的.po文件
* 最后.po文件需要使用msgfmt编译为.mo文件以用作发布
* 使其运行需要使用UNIX操作系统中的用户需要修改环境变量中的`LC_MESSAGES`或`LANG`，程序将自动从相应的.mo文件中读取语言信息

使用方法:
```
在使用gettext()方法的时候通常以标记别名_的形式使用
如printf(gettext("name is %s. \n"), first_name);
可以写作printf(_("name is %s.\n"), first_name);
```

---

参考资料:
官方网站[跳转](https://www.gnu.org/software/gettext/)
`https://www.gnu.org/software/gettext/`
获取[跳转](https://ftp.gnu.org/pub/gnu/gettext/gettext-0.20.1.tar.gz)
`https://ftp.gnu.org/pub/gnu/gettext/gettext-0.20.1.tar.gz`
社区[跳转](https://savannah.gnu.org/projects/gettext/)
`https://savannah.gnu.org/projects/gettext/`
文档[跳转](https://www.gnu.org/software/gettext/manual/gettext.html)
`https://www.gnu.org/software/gettext/manual/gettext.html`
