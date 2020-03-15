---
title: Coding-1
date: 2020-03-15 16:43:22
tags: 随笔
categories: [软件,Coding]
---

<center><strong>ASCII-1</strong></center>

<!-- more -->

### 编码(coding)-1

* ASCII (American Standard Code for Information Interchange)
* 美国信息交换标准代码
* 美国标准信息交换代码是由美国国家标准学会 (American National Standard Institute/可简称为ANSI)所制定的标准
* 是一种标准的单字节字符编码方案，用于基于文本的数据
* 后来它被国际标准化组织 (International Organization for Standardization)，可简称为ISO，定为国际标准，称为ISO 646标准
* 适用于所有拉丁文字字母
* ASCII标准表可参考下方文献
* 其存在的目的是为统一计算机领域的所有编码规则

**编码**

* 在计算机中，所有的数据在存储和运算时都要使用二进制数表示(因为计算机用高电平和低电平分别表示1和0)
* 例如，像a，b，c，d这样的52个字母(包括大写)以及0，1等数字还有一些常用的符号(例如`*`，`#`，`@`等)在计算机中存储时也要使用二进制数来表示
* 而具体用哪些二进制数字表示哪个符号，当然每个人都可以约定自己的一套，即为编码

---

* ASCII码使用指定的7位或8位的二进制组合来表示128或256种可能的字符
* 标准ASCII码也叫基础ASCII码，使用7位二进制数(剩下的1位二进制为0)来表示所有的大写和小写字母，数字0到9，标点符号，以及在美式英语中使用的特殊控制字符
* 按照指定的格式与规则给输入输出的信息进行指定的编码，本质就是将计算机内一切的数据和信息转换为二进制代码的不同组合，以便给予机器并让机器执行相应的指令

---

**ASCII码的基本规律:**

* 0～31及127(共33个)是控制字符或通信专用字符(其余为可显示字符)，如控制符: LF(换行),CR(回车),FF(换页),DEL(删除),BS(退格),BEL(响铃)等
> 通信专用字符: SOH(文头),EOT(文尾),ACK(确认)等
> ASCII值为8,9,10和13分别转换为退格，制表，换行和回车字符
> 它们并没有特定的图形显示，但会依不同的应用程序，而对文本显示有不同的影响
* 32～126(共95个)是字符(32是空格），其中48～57为0到9十个阿拉伯数字
* 65～90为26个大写英文字母，97～122号为26个小写英文字母，其余为一些标点符号，运算符号等

* 同时还要注意，在标准ASCII中，其最高位(b7)用作奇偶校验位
> 所谓奇偶校验，是指在代码传送过程中用来检验是否出现错误的一种方法，一般分奇校验和偶校验两种
> 奇校验规定: 正确的代码一个字节中1的个数必须是奇数，若非奇数，则在最高位b7添1
> 偶校验规定: 正确的代码一个字节中1的个数必须是偶数，若非偶数，则在最高位b7添1
* 后128个称为扩展ASCII码
> 许多基于x86的系统都支持使用扩展(或"高")ASCII
> 扩展ASCII码允许将每个字符的第8位用于确定附加的128个特殊符号字符，外来语字母和图形符号

---

**涉及概念:**

* 点阵
* 字库
* 点阵字库/字模(数据)
* 格式问题(UCS-2等)
* 码点
* 编码
* Little endian/Big endian

---

**其它的编码系统**

* 非ASCII编码
* Unicode
* UTF-8
* 中文编码

---

### 参考文献

**中文维基**

* ASCII[跳转](https://zh.wikipedia.org/wiki/ASCII)
> `https://zh.wikipedia.org/wiki/ASCII`
* 分类:字符集[跳转](https://zh.wikipedia.org/wiki/Category:%E5%AD%97%E7%AC%A6%E9%9B%86)
> `https://zh.wikipedia.org/wiki/Category:%E5%AD%97%E7%AC%A6%E9%9B%86`
* 分类: 编码[跳转](https://zh.wikipedia.org/wiki/%E7%BC%96%E7%A0%81)
> `https://zh.wikipedia.org/wiki/%E7%BC%96%E7%A0%81`
* 字符编码[跳转](https://zh.wikipedia.org/wiki/%E5%AD%97%E7%AC%A6%E7%BC%96%E7%A0%81)
> `https://zh.wikipedia.org/wiki/%E5%AD%97%E7%AC%A6%E7%BC%96%E7%A0%81`
* 晶体结构[跳转](https://zh.wikipedia.org/wiki/%E6%99%B6%E4%BD%93%E7%BB%93%E6%9E%84)
> `https://zh.wikipedia.org/wiki/%E6%99%B6%E4%BD%93%E7%BB%93%E6%9E%84`

**百度百科**
> [跳转](https://baike.baidu.com/item/ASCII/309296?fr=aladdin)-`https://baike.baidu.com/item/ASCII/309296?fr=aladdin`
> [跳转](https://baike.baidu.com/item/%E7%BC%96%E7%A0%81%E5%8E%9F%E7%90%86/20837166?fr=aladdin)-`https://baike.baidu.com/item/%E7%BC%96%E7%A0%81%E5%8E%9F%E7%90%86/20837166?fr=aladdin`

**CSDN**
> [跳转](https://baike.baidu.com/item/%E7%BC%96%E7%A0%81%E5%8E%9F%E7%90%86/20837166?fr=aladdin)-`https://blog.csdn.net/exbob/article/details/6532772?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task`
> [跳转](https://blog.csdn.net/yuanwofei/article/details/12846331)-`https://blog.csdn.net/yuanwofei/article/details/12846331`
> [跳转](https://blog.csdn.net/Deft_MKJing/article/details/79460485)-`https://blog.csdn.net/Deft_MKJing/article/details/79460485`

---



