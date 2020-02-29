---
title: LFS-8
date: 2020-03-01 04:40:11
tags: [GNU/Linux,随笔]
categories: [软件,GNU]
---

## LFS-8

---

### LFS-v6.3基本程序一览

* LFS-v6.3内软件目录(包含版本与章节)
* 不包含[GNU 工具链]内程序

**参考资料:**
* EN-LFS-v6.3[跳转](http://www.linuxfromscratch.org/lfs/downloads/6.3/)
> `http://www.linuxfromscratch.org/lfs/downloads/6.3/`

* CN-6.6非官方[跳转](http://www.ha97.com/book/lfs-book-6.6/)
> `http://www.ha97.com/book/lfs-book-6.6/`

---

**临时主机程序目录**

5.13. Ncurses-5.6 
5.14. Bash-3.2
5.15. Bzip2-1.0.4
5.16. Coreutils-6.9
5.17. Diffutils-2.8.1 
5.18. Findutils-4.2.31
5.19. Gawk-3.1.5
5.20. Gettext-0.16.1 
5.21. Grep-2.5.1a
5.22. Gzip-1.3.12 
5.23. Make-3.81
5.24. Patch-2.5.4
5.25. Perl-5.8.8
5.26. Sed-4.1.5
5.27. Tar-1.18
5.28. Texinfo-4.9
5.29. Util-linux-2.12r

---

**目标主机程序目录**

6.13. Berkeley DB-4.5.20
6.14. Sed-4.1.5
6.15. E2fsprogs-1.40.2 
6.16. Coreutils-6.9
6.17. Iana-Etc-2.20
6.18. M4-1.4.10 
6.19. Bison-2.3 
6.20. Ncurses-5.6 
6.21. Procps-3.2.7
6.22. Libtool-1.5.24
6.23. Perl-5.8.8
6.24. Readline-5.2 
6.25. Zlib-1.2.3 
6.26. Autoconf-2.61 
6.27. Automake-1.10 
6.28. Bash-3.2 
6.29. Bzip2-1.0.4
6.30. Diffutils-2.8.1
6.31. File-4.21
6.32. Findutils-4.2.31 
6.33. Flex-2.5.33
6.34. GRUB-0.97
6.35. Gawk-3.1.5
6.36. Gettext-0.16.1 
6.37. Grep-2.5.1a
6.38. Groff-1.18.1.4
6.39. Gzip-1.3.12
6.40. Inetutils-1.5 
6.41. IPRoute2-2.6.20-070313 
6.42. Kbd-1.12 
6.43. Less-406
6.44. Make-3.81
6.45. Man-DB-2.4.4
6.46. Mktemp-1.5
6.47. Module-Init-Tools-3.2.2
6.48. Patch-2.5.4
6.49. Psmisc-22.5
6.50. Shadow-4.0.18.1 
6.51. Sysklogd-1.4.1 
6.52. Sysvinit-2.86
6.53. Tar-1.18 
6.54. Texinfo-4.9 
6.55. Udev-113
6.56. Util-linux-2.12r
6.57. Vim-7.1

---

**最终阶段程序**

7.2. LFS-Bootscripts-6.3 
Linux-2.6.22.5

---

## 相关指令参考

* patch
* sed
* ld
* strip

---

### patch命令

* Linux patch命令用于修补文件(为文件打上补丁)
> patch指令让用户利用设置修补文件的方式，修改，更新原始文件
> 倘若一次仅修改一个文件，可直接在指令列中下达指令依序执行
> 如果配合修补文件的方式则能一次修补大批文件
> 这也是Linux系统核心的升级方法之一

* 语法:
> `patch [参数] [选项] [原始文件 <修补文件>] 或 path [-p <剥离层级>] < [修补文件]`
> 具体参考: https://www.runoob.com/linux/linux-comm-patch.html

* 实例:
* `$ patch -Np1 i ../expect-5.43.0-spawn-1.patch`
> 将`expect`工具打上补丁`expect-5.43.0-spawn-1.patch`

---

### sed命令

* Linux sed 命令的作用是利用脚本来处理文本文件
* sed可依照脚本的指令来处理，编辑文本文件
* sed主要用来自动编辑一个或多个文件，简化对文件的反复操作，编写转换程序等

* 命令语法:
> `sed [-hnV][-e<script>][-f<script文件>][文本文件]`
> 具体参考: https://www.runoob.com/linux/linux-comm-sed.html

* 实例:
* 利用sed命令来确保在非bootstrap编译时也同样使用`-fomit-frame-pointer`选项，以保持一致性
```
$ cp -v gcc/Makefile.in{,.tmp} &&
sed 's/^XCFLAGS =$/& -fomit-frame-pointer/' gcc/Makefile.in.tmp \
> gcc/Makefile.in
```

---

### ld命令

* ld 命令是二进制工具集GNU Binutils的一员，是GNU的链接器，用于将目标文件与库链接为可执行文件或库文件

* 命令语法:
> `$ ld [OPTIONS] OBJFILES`

* 实例:
* 链接目标文件生成可执行文件
* 给定C++目标文件`test.o`与`main.o`，生成可执行文件`test.out`
```
$ ld /usr/lib64/crt1.o /usr/lib64/crti.o /usr/lib64/crtn.o &&
/usr/lib/gcc/x86_64-redhat-linux/4.8.5/crtbegin.o /usr/lib/gcc/x86_64-redhat-linux/4.8.5/crtend.o &&
-L/usr/lib/gcc/x86_64-redhat-linux/4.8.5 &&
-L/usr/lib64 -L/usr/lib -lstdc++ -lm -lgcc_s -lc -lgcc  main.o test.o -o test.out
```

> 具体参考:
> https://www.gnu.org/software/binutils/
> https://www.linux.org/docs/man1/ld.html
> https://blog.csdn.net/K346K346/article/details/89088652
> https://dablelv.blog.csdn.net/article/details/88094902
> http://stackoverflow.com/questions/14179969/whats-the-different-between-l-libpath-and-etc-ld-so-conf-configure-the-libpat

* ld和ld.so的区别[跳转](https://www.cnblogs.com/foohack/p/4105717.html)
> `https://www.cnblogs.com/foohack/p/4105717.html`

---

### Strip

* 从特定文件中剥掉一些符号信息和调试信息，使文件变小
* strip - Discard symbols from object files(from man strip)

* 具体语法:
> `$ strip [-xxx bfdname |--xxx=bfdname]`
> strip 之后的任何选项都是自定义参数，这里将不会做过多阐述
> 参考自: https://blog.csdn.net/qq_37858386/article/details/78559490

* 实例:
* 清理`/tools/lib`内所有的debug文件
> `$ strip --strip-debug /tools/lib/*`

---



