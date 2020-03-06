---
title: LSP-2.2
date: 2020-03-07 01:59:36
tags: [软件,OS,GNU/Linux]
categories: [软件,OS]
---

<center><strong>UNIX/Linux系统调用与库函数调用的执行检查与错误处理</center></strong>
<center><strong>UNIX/Linux-2.2</center></strong>
<!-- more --> 

## LSP-2.2

---

### Linux/UNIX-2.1

* 系统编程概念-2

---

**涉及概念一览:**

* 库函数基本检查
* 系统调用检查与错误处理
* 库函数调用检查与错误处理

---

### 库函数

* 库函数即为存在于C 标准库内的任何函数，也可以称其为函数
> 设计库函数的目的是为了提供比底层系统调用更方便的调用接口

* 标准C语言函数库: GNU C 语言函数库(Glibc)
> 标准C语言函数库的实现跟随UNIX的实现而异
> GNU C语言函数库即为Linux上最常用的实现

* 除了标准的函数之外通常还有其它的拓展函数uClibc与dietlibc
> uClibc: htttp://www.ulibc.org
> dietlibc: http://www.fefe.de/detlibc

* 因为Linux开发的大多数开发都只能用到Glibc，所以这里将不会对其它的拓展函数库进行过多讨论

* 查看当前系统的Glibc版本
> 直接运行其glibc的共享库文件(可执行文件)，以获取版本
> `$ /lib/libc.so.6`

* 确定改库存放位置的方法之一:
> 针对某个与glibc动态链接的可执行文件，运行ldd程序
> 然后再检查已输出的库依赖列表，便能发现glibc共享库所处于的位置
> `$ ldd myprog | grep libc`

---

* 应用程序可以通过测试常量和调用函数库这两种方法来确定系统所安装的glibc版本及其详细信息
> 从版本2.0开始，glibc定义了两个常量`__GLIBC__`和`__GLIBC_MINOR__`，以供程序再编译时(在`#ifdef`语句中)测试使用
> 为了避免在同步机器上造成的版本不同而产生的参数差异所带来的种种问题，可以在程序内调用`gnu_get_libc_version()`来确定运行时的glibc版本

```
#include <gnu/libc-version>

const char *gnu_get_libc_version(void);
```

* 而对于获取glibc版本信息，还有一种方法，即为使用`confstr()`函数来获取(glibc特有的)`_CS_GNU_LIBC_VERSION`配置变量的值
> 其返回的字符串与上述实例相同

---

### 如何处理来自系统调用的错误与如何处理来自库函数的错误

* 几乎每个系统调用和库函数都会返回某类状态值，用以表明调用成功与否
> 如果想要深入的了解调用是否成功，必须检查对状态值进行检查
> 若调用失败，则采取相应行动
> 所以让程序显示错误消息，以防止有意想不到的时间发生，是非常有必要的
> 但是还有少数几个系统调用函数在调用时从不会失败(例如`getppid()`总是能成功返回`进程的ID`，而`_exit()`总能终止进程，则无需对此类系统调用的返回值进行检查)

---

**如何处理来自系统调用的错误:**

* 每个系统调用的手册页记录有调用可能的返回值，并指出了哪些值表示错误
> 通常，返回值为-1则表示出错，当处于此种情况下，可以使用下列代码对系统调用进行检查

```
fd = open(pathname, flags, mode); /* system call to open a file */
if (fd == -1) {
/* Code to handle the error */
}
...
if (close(fd) == -1) {
/* Code to heandle the error */
{
```

* 当系统调用失败时，会将全局整形变量`errno`设为一个正值，以标识具体的错误
> 程序(`#include`)包含`<errno.h>`头文件，该文件提供了对`errno`的声明，以及一组针对各种错误编号而定义的常量
> 所有这些符号名都以子字母E打头，在每个手册页内标题为`ERRORS`的章节内，都刊载有一份相应系统调用可能返回的`errno值`列表

* 这里是利用`errno`来诊断系统调用错误的一个简单实例:

```
cnt = read(fd, buf, numbytes);
if (cnt == -1) {
if (errno == EINTR)
fpintf(stderr, "read was interrupted by a signal\n")
else {
/* Some other error occurred */
}
{
```

* 如果调用系统函数和函数库成功，`errno`绝不会被重置为0，故此改变了值不为0，还有可能是因为之前的调用失败造成的
> 此外，`SUSv3`允许在函数调用成功时，将`errno`设置为非零值(但是基于没有函数会这么做)
> 因此，在进行错误检查时，必须检查首先检查函数的返回值是否表明调用出错，然后再检查`errno`确定错误原因
> 少数系统调用(比如`getpriority()`)在调用成功后，也会`返回-1`
> 所以在要判断此类系统调用是否发生错误，应在调用前将`errno`设置为0，并在调用后进行检查(以上所描述的手法同样适用于某些库函数)

* 系统调用失败后，常见的做法之一就是根据`errno`值来打印错误消息，提供的库函数`perror()`和`strerror()`，就是处于此目的
> 此实例中函数`perror()`会打印出其`msg参数`所指向的字符串，紧跟一条与当前`errno值`相对应的消息

```
#include <stdio.h>

void perror(const char *msg);
```

* 以下是对系统调用错误进行错误的一种简单方式:

```
fd = open(pathname, flags, mode);
if (fd == -1) {
perror("open")
exit(EXIT_FAILURE);
}
```

* 函数`strerror()`会针对其`errnum`参数中所给定的错误号，返回相应的错误字符串

```
#include <stdio.h>
char *strerror(int errnum);
```

* 由`strerror()`所返回的字符串可以是静态分配的，这意味着后续对`sterror()`的调用可能会覆盖该字符串
> 若无法识别`errnum`所含的错误编号，则`strerror()`会返回`"Unknown error nnn"`形式的字符串
> 在某些其它的视线中，在这种情况下，`strerror()`会返回`NULL`

* 由于`perror()`和`sterror()`都属于对语言环境敏感(locale-sensitive)的函数，故而错误描述中使用的都是本地语言

---

**处理来自库函数的错误**

* 不同的库函数在调用发生错误时，所返回的数据类型和值也各不相同(可以参见每个函数的手册页)
* 从错误的角度来讲，可以分为以下几类:

1. 某些库函数返回错误信息的方式与系统调用完全相同，则`返回值为-1`，伴之以`errno号`来标识具体错误
> `remove()`便是其中一例，可使用该库函数来删除文件(调用`unlink()`相同调用)或目录(调用`rmdir()`相同调用)
> 对此类函数所发生的错误进行诊断，其方式与系统调用完全相同
2. 某些库函数在出错时会`返回-1`之外的其他值，但仍会设置`errno`来表明具体的出错情况
> 例如，`fopen()`在出错时会返回一个`NULL指针`，还会根据出错的具体底层相同调用来设置`errno`
> 函数`perror()`和`sterror()`都可用来诊断此类错误
3. 还有一些函数根本不使用`errno`，对此类函数来说，确定错误存在与否及其起因的方法各不相同
> 同样可见诸于相应函数的手册页中，不应使用`errno`，`perror()`或`strerror()`来诊断错误

---

### 参考文献:

* Linux/UNIX系统编程(上册)
* 参考自原书3.3-3.4章节

---



