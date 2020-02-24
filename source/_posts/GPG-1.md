---
title: GNU Privacy Guard/GPG-1
date: 2020-02-24 18:17:18
tags: [随笔,GNU/Linux]
categories: [软件,Password]
---

## GNU Privacy Guard/GPG-1

### 简要概述与参考资料整理

* 数据完整性(Data integrity)

* 使用工具:
* GPG(GNU Privacy Guard)
> Linux GPG
> GNU PG

---

### 命令简述:

* 生成密钥
> `$gpg --gen-key`
> 安装提示对密钥进行配置

* 列出密钥
> `$gpg --list-keys`

* 删除密钥
> `gpg --delete-key [用户ID]`

* 输入密钥
> `gpg --import [密钥文件]`

* 加密文件
> `gpg --recipient [用户ID] --output [file name] --encrypt [file name]`

* 解密并输出内容
> `gpg [file name]`

* 文件签名(二进制存储)
> `gpg --sign [file name]`

* 文件签名(ASCII码存储)
> `gpg --clearsign [file name]`

* 生成单独的签名文件(二进制存储)
> `gpg --detach-sign [file name]`

* 生成单独的签名文件(ASCII码存储)
> `gpg --armor --detach-sign [file name]`

* 验证签名
> `gpg --verify [file name].[asc] [file name]`

* 等等

---

**其它说明:**

* 方括号为可选参数
* 这里的数据完整性以数据签名实现
* 压缩所选文件或目录并进行哈希加密实现数字签名
* 不进行压缩进行数字加密

---

**相关概念:**

* GPG
* PGP
* GPG2
* RSA加密算法(对称加密算法)
* 数据校检
* 数字签名
* 数据完整性
* 软件包签名
* 压缩文件签名
* 数据库数据完整性
* 文件目录数据完整性

---

### 参考资料:

**以下内容参考自中文维基与百度百科:**

**中文维基**

* 数据完整性[跳转](https://zh.wikipedia.org/wiki/%E6%95%B0%E6%8D%AE%E5%AE%8C%E6%95%B4%E6%80%A7)
> `https://zh.wikipedia.org/wiki/%E6%95%B0%E6%8D%AE%E5%AE%8C%E6%95%B4%E6%80%A7`

* 数字签名[跳转](https://zh.wikipedia.org/wiki/%E6%95%B8%E4%BD%8D%E7%B0%BD%E7%AB%A0)
> `https://zh.wikipedia.org/wiki/%E6%95%B8%E4%BD%8D%E7%B0%BD%E7%AB%A0`

**百度百科**

* 数据完整性[跳转](https://baike.baidu.com/item/%E6%95%B0%E6%8D%AE%E5%AE%8C%E6%95%B4%E6%80%A7)
> `https://baike.baidu.com/item/%E6%95%B0%E6%8D%AE%E5%AE%8C%E6%95%B4%E6%80%A7`

* 数据校检[跳转](https://baike.so.com/doc/741565-784957.html)
> `https://baike.so.com/doc/741565-784957.html`

---

**参考文献:**

* Linux下使用GPG加密解密的说明及示例[跳转](https://www.linuxidc.com/Linux/2015-02/113015.htm)
> `https://www.linuxidc.com/Linux/2015-02/113015.htm`

* 如何在Linux下使用GPG(GnuPG)加密及解密[跳转](https://jingyan.baidu.com/album/3d69c5513244a7f0ce02d751.html?picindex=1)
> `https://jingyan.baidu.com/album/3d69c5513244a7f0ce02d751.html?picindex=1`

* GPG简要介绍[跳转](http://www.ruanyifeng.com/blog/2013/07/gpg.html)
> `http://www.ruanyifeng.com/blog/2013/07/gpg.html`

* Gnu隐私卫士(GnuPG)袖珍HOWTO(中文版)[跳转](https://www.gnupg.org/howtos/zh/index.html)
> `https://www.gnupg.org/howtos/zh/index.html`

---

