---
title: GNU Portable Threads/Pth
date: 2020-02-02 01:57:11
tags: [1.认识与概述,GNU/Linux]
categories: [软件,GNU]
---

### GNU Portable Threads 第一章节

**GNU 可移植线程库 Pth**

**概述:**
* GNU计划重要的一部分
* GNU Pth 是用于UNIX平台下基于POSIX与ANSI C的用户空间线程库
* GNU Pth还包含了POSIX线程的API，以达成向后兼容的目的

GNU Pth使用到内核空间线程的N:1映射，所以说调度完全将完全由GNU Pth库进行
内核将不会干涉用户空间中任何数量的线程，所以利用不到SMP[^1]所拥有的机制，因为SMP必须由内核派遣
[^1]: 均衡多处理架构

**存在目的:**
* GNU Pth的目的是针对任意线程的处理达到高度的可移植性
* 其次是为了让多线程应用提供基于优先级的调度
---

**参考资料:**

官方网站[跳转](https://www.gnu.org/software/pth/)
`https://www.gnu.org/software/pth`

官方手册[跳转](https://www.gnu.org/software/pth/pth-manual.html)
`https://www.gnu.org/software/pth/pth-manual.html`

多线程库列表[跳转](https://www.gnu.org/software/pth/related.html)
`https://www.gnu.org/software/pth/related.html`

[多线程库文档，包含了Unix系统中所有对于已知多线程库的调用](https://www.gnu.org/software/pth/related.html)
`https://www.gnu.org/software/pth/related.html`

关于OSSP pth[跳转](http://www.ossp.org/pkg/lib/pth/)
`http://www.ossp.org/pkg/lib/pth`

论文引用:
[对于GNU pth的使用与描述](http://heather.cs.ucdavis.edu/~matloff/pth.html)
`http://heather.cs.ucdavis.edu/~matloff/pth.html`
