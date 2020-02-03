---
title: GNU Data Display Debugger
date: 2020-02-02 16:25:37
tags: [GNU/Linux,1.认识与概述]
categories: [软件,GNU]
---

### GNU Data Display Debugger

**GNU 调试器前端 DDD**

**概述:**

DDD:
* DDD基于GPL许可证发行
* DDD是GNU计划的一个重要的组成部分
* DDD主要用于Unix系统,并且有许多开源插件对其使用性的补充
* GNU DDD是一个用于数据显示的调试器前端(Debugger front-end)，它使用motif工具包实现GUI
* 应用于诸如GDB,DBX,JDB,XDB,多种语言调试器和bash等命令行调试器的调试器前端，也包括GNU Make调试器等用于调试器的调试器前端
* DDD拥有GUI前端的功能，可以查看源文本及其交互式图形数据的显示，将数据结构以图形化显示

GCL:
* 调试器前端就是所指调试器所使用的命令行解释器/命令行界面(CLI)，这里所指的调试器前端就是DDD
* 一个好的CLI可以最大程度的提高可移植性并最大程度地减少资源消耗
* 而最让开发者们青睐的还得是具备GUI的CLI，所以有一些GUI调试器的前端被设计成与各种GLI相兼容，还有一些GUI则针对某一个特定的GLI
---

**参考资料:**

文档[跳转](https://www.gnu.org/software/ddd/manual/html_mono/ddd.html)
`https://www.gnu.org/software/ddd/manual/html_mono/ddd.html`

官网[跳转](https://www.gnu.org/software/ddd/)
`https://www.gnu.org/software/ddd/`

社区[跳转](http://savannah.gnu.org/svn/?group=ddd)
`http://savannah.gnu.org/svn/?group=ddd`

[参考资料:](https://lists.gnu.org/archive/html/ddd/2009-02/msg00001.html)
`https://lists.gnu.org/archive/html/ddd/2009-02/msg00001.html`
