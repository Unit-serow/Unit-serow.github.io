---
title: UNIX/PIPE-1
date: 2020-03-05 14:37:00
tags: [随笔,UNIX]
categories: [软件,UNIX]
---

<center><strong>UNIX-PIPES概述</strong></center>

<!-- more -->

## UNIX/PIPE-1

---

### Unix-Pipeline/Pipes-1

**概述:**

* 管道(Pipeline)是一系列将标准输入输出链接起来的进程
* 其中每一个进程的输出被直接作为下一个进程的输入
* 每一个链接都由匿名管道实现
* 管道中的组成元素也被称作过滤程序
* 通常被用于类Unix操作系统(以及一些其他借用了这个设计的操作系统，如Windows)中
* 其他操作系统的这个特色源自于Unix，例如Taos和MS-DOS
> 最终成为软件工程的管道与过滤器设计样本
* 这个概念是由道格拉斯·麦克罗伊为Unix命令行发明的，因与物理上的管道相似而得名
* UNIX管道技术需要注意的一点就是需要将管道与管线区分开来(两种截然不同的概念)

---

### 具体描述:

**管道概念:**

1. 管道是用于将一系列的标准输入输出指令(代码)链接起来，从而形成进程的最基本条件
2. 并且被链接的每一个进程的输出被直接作为下一个进程的输入
**还可以将其描述为:**
1. 管道是将一系列标准输入输出链接起来的进程
2. 其中每一个进程的输出被直接作为下一个进程的输入

3. 其中每一个链接都由匿名管道实现
4. 管道中的组成元素也被称作过滤程序

* 其概念模型非常类似于现实世界种的管道

* 该图片描述了某一文字终端上一个包含三个程序的管道:

<img src="/images/KVM-1.png" width="40%" height="40%">

---

**管线:**

* 是指将计算机指令处理过程拆分为多个步骤
* 并通过多个硬件处理单元并行执行来加快指令执行速度

* 亦可称之为流水线
> 因为其具体执行过程类似工厂中的流水线，并因此得名
> 可以将计算机指令比喻为流水线传送带上的产品
> 而各个硬件处理单元就是流水线旁的工人
> 每个不同的产品都需要细分为几个互不相同的部门来实现其各部件的所需
> 所以流水线中所属部门不同的工人会为了同一个产品而同时工作
---
* 微处理器
* 在使用流水线的处理器中一个指令不是在处理器的一个定时器信号中完成的
> 而是被分到多个信号中去完成，但是与此同时多个指令的分任务被同时处理
* 由于这些分任务比整个指令要简单，因此可以通过使用流水线提高定时器频率
> 虽然每个指令需要多个信号后才能完成
> 但是通过多个指令的并行运算每个信号内一个指令可以完成
> 因此通过这个方法整个速度可以提高
---
* 流水线级
* 一条流水线的每个分步骤被称为流水线级
> 它们被流水线寄存器分开除指令流水线外在现代系统中还有其它流水线
> 比如用来计算浮点数的算术流水线
---
* 管线危障(pipeline hazards)
* 假如，一个指令在执行的时候，需要等待流水线上前一个指令先执行完毕的话
> 那么这两个指令相互之间彼此有依赖关系
> 这可能导致流水线冲突的现象发生
> 即为管线危障
* 常见情况可分为四种: 资源冲突/数据冲突(指令层的数据冲突/传输层的数据冲突)/控制流冲突
* 通过分支预测器可以避免控制冲突
> 在这里处理器预测性地继续运算，直到正式预测是正确为止

---

**网络管线:**

* Unix哲学: "一切皆文件"
> netcat和socat这样的工具可以将管道连接到TCP/IP套接字

---

**相关概念:**

* 管道(UNIX)
* 具名管道
* 命名管道
* 匿名管道
* 匿名命名管道
* 哈特曼管道
* 管线(流水线)
* 管线/流水线(计算机)
* 管线危障(pipeline hazards)
* 重定向(计算机)
* `tee指令`
> 该程序用于从管线内取出数据
* XML管道即为处理XML的管线
* 网络管线
* UNIX
* 进程间通信
* 数字通信技术
> 计算机通信技术
* 管道协议
* 并发计算
* 协同控制

---

### 参考资料:

* EN-System Interfaces[跳转](https://pubs.opengroup.org/onlinepubs/9699919799/functions/pipe.html)
* 单一UNIX规范第7期，由国际开放标准组织发布
> `https://pubs.opengroup.org/onlinepubs/9699919799/functions/pipe.html`

* EN-Pipes: A Brief Introduction by The Linux Information Project (LINFO)[跳转](http://www.linfo.org/pipe.html)
> `http://www.linfo.org/pipe.html`

* 获取管道的doc文案: http://www.cs.rit.edu/~swm/history/DTSS.doc
---
* 以下内容参考自中文维基:

* CN-分类:
> 进程通信[跳转](https://zh.wikipedia.org/wiki/Category:%E8%BF%9B%E7%A8%8B%E9%97%B4%E9%80%9A%E4%BF%A1)
> 进程间通信[跳转](https://zh.wikipedia.org/wiki/%E8%A1%8C%E7%A8%8B%E9%96%93%E9%80%9A%E8%A8%8A)
> `https://zh.wikipedia.org/wiki/Category:%E8%BF%9B%E7%A8%8B%E9%97%B4%E9%80%9A%E4%BF%A1`
> `https://zh.wikipedia.org/wiki/%E8%A1%8C%E7%A8%8B%E9%96%93%E9%80%9A%E8%A8%8A`

* CN-分类: UNIX[跳转](https://zh.wikipedia.org/wiki/Category:Unix)
> `https://zh.wikipedia.org/wiki/Category:Unix`

* CN-分类: 并发计算[跳转](https://zh.wikipedia.org/wiki/Category:%E5%B9%B6%E5%8F%91%E8%AE%A1%E7%AE%97)
> `https://zh.wikipedia.org/wiki/Category:%E5%B9%B6%E5%8F%91%E8%AE%A1%E7%AE%97`

* CN-分类: 协同控制[跳转](https://zh.wikipedia.org/wiki/Category:%E5%8D%94%E5%90%8C%E6%8E%A7%E5%88%B6)
> `https://zh.wikipedia.org/wiki/Category:%E5%8D%94%E5%90%8C%E6%8E%A7%E5%88%B6`

* EN-分类: 指令处理[跳转](https://en.wikipedia.org/wiki/Category:Instruction_processing)
> `https://en.wikipedia.org/wiki/Category:Instruction_processing`

---

* CN-维基百科-点对点隧道协议: https://zh.wikipedia.org/wiki/%E9%BB%9E%E5%B0%8D%E9%BB%9E%E9%9A%A7%E9%81%93%E5%8D%94%E8%AD%B0
* CN-维基百科-管道机制: https://zh.wikipedia.org/wiki/%E7%AE%A1%E9%81%93_(Unix)
* CN-维基百科-管道流: https://zh.wikipedia.org/wiki/%E6%B5%81%E6%B0%B4%E7%BA%BF_(%E8%AE%A1%E7%AE%97%E6%9C%BA)
* CN-维基百科-IDC: https://zh.wikipedia.org/wiki/%E6%95%B0%E6%8D%AE%E4%B8%AD%E5%BF%83
* CN-维基百科-管线: https://zh.wikipedia.org/wiki/%E6%B5%81%E6%B0%B4%E7%BA%BF_(%E8%AE%A1%E7%AE%97%E6%9C%BA)
* CN-维基百科-命名管道: https://zh.wikipedia.org/wiki/%E5%91%BD%E5%90%8D%E7%AE%A1%E9%81%93
* EN-维基百科-管道(计算机): https://en.wikipedia.org/wiki/Pipeline_(computing)

---



