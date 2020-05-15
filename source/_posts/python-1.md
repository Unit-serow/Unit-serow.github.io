---
title: python-1
date: 2020-05-16 00:57:48
tags: 随笔
---

<center><strong>Python-1</strong></center>

<!-- more -->

* Python-1：

python中的标准数据类型：numbers（数字）、string（字符串）、list（列表）、tuple（元组）、dictionary（字典）

number：int（符号整形）、long（长整型）、float（浮点型）、complex（复数）

string：python中的单字符被视为字符串，所以没有单字符概念，如果要精确截取某个字符可以直接访问其内存地址

list：python最基本的数据结构，没有之一，python当中有六个序列的内置类型，但最常见且常用的只有列表和元组，python的列表类似于c或其它程序语言之间的数组

tuple：元组和列表相似，只不过元素之间的元素不能被修改，可以将tuple视为只读的的list

dictionary：字典是另一种可变容器模型，由键与值所构成（有如：key=>value，即key:value），是python的一大特性之一，其使用方法非常自由，可以存储任意对象，简写为dict，自由到什么地步呢，其值可以存储任何数据类型，包括数组（列表）、元组或各类字符串

字典值可以没有限制地取任何python对象，既可以是标准的对象，也可以是用户定义的，但键不行，键的赋值原则与内存栈相同

python内的数学库：math、cmath，并且使用import进行导入

python的条件判断标识符：if、if...else...、if...elif...elif...else...、if not...

python的循环运算标识符：while、while...else、for、while...while、for...for

python的中止运算标识符：break、continue、pass

运算符是任何程序语言的逻辑核心，对于计算机来说通常的结果只有两个，即真或假（ture & false），还可将其称之为布尔（bool）运算符

---

python的时间函数库为time()，时间戳为一秒，时间跨度为1970年~2038年，当前的时间戳为1589542517.53，python用时间元组来表示更直观的时间，也就是将时间戳的浮点数利用类似于localtime之类的函数转换称时间元组

有如：time = time.struct_time(tm_year=2020, tm_mon=5, tm_mday=15, tm_hour=19, tm_min=38, tm_sec=39, tm_wday=4, tm_yday=136, tm_isdst=0)

python中对于自定义函数的使用也是非常之方便，用关键字def定义，后接标识符于圆括号()，圆括号之间用于定义参数，函数内容以冒号起始并且需要缩进，以return[表达式]结束函数，需要选择性的返回一个值给调用方，否则reture返回none

python中类型属于对象而变量没有类型

python中，strings、tuples和numbers是不可更改的对象，而list、dict等则是可以修改的对象，进行传参时需要去注意一下

python中拥有模块概念，也就是以.py后缀结尾的python源文件，可以将某一个单独的函数封装在一个模块当中，使用import导入，即import module1[, module2[,... moduleN]]，还可以对模块中的任意函数进行调用，有如：模块名.函数名

当解释器遇到 import 语句，如果模块在当前的搜索路径就会被导入，搜索路径是一个解释器会先进行搜索的所有目录的列表，如想要导入某一个模块，需要把导入模块的命令放在脚本的顶端，并且每个模块只能导入一次且只会被导入一次

python还支持只导入模块中的某一部分而并非导入整个模块，使用from...import...模块，比如导入fib模块的fibonacci函数，有如：from fib import fibonacci，from modname import *则是导入模块中的所有内容

Python 解析器对模块位置的搜索顺序是：当前目录、如果不在当前目录，Python则搜索在shell变量PYTHONPATH下的每个目录、如果都找不到，Python会察看默认路径、UNIX下，默认路径一般为/usr/local/lib/python/

模块搜索路径存储在system模块的sys.path变量中，变量里包含当前目录，PYTHONPATH和由安装过程决定的默认目录

---

关于PYTHONPATH变量，作为环境变量，PYTHONPATH由装在一个列表里的许多目录组成

PYTHONPATH 的语法和shell变量PATH的一样，有如：set PYTHONPATH=/usr/local/lib/python（UNIX系统下比较典型的PYTHONPATH存储目录）

关于python的命名空间，命名空间是一个包含了所有变量的键与其所对应的值的字典，键则为标识符，值就是值

python表达式可以访问局部命名空间和全局命名空间中的变量，同时如果一个局部变量和一个全局变量重名，则局部变量会覆盖全局变量，每个函数都有自己的命名空间，类的方法的作用域规则和通常函数的相同

python在识别某一个变量是全局的还是局部的时候会默认在函数内被赋值的变量皆为局部的，所以如果需要给全局变量赋值时必须使用global语句，标识global VarName后解释器便会人为VarName是一个全局变量

有一个比较重要的函数，dir()函数，它的内容是一个排好序的字符串列表，其间所表示的是模块内的所有函数（无论是默认的还是自定义的），其间特殊字符串变量__name__指向模块的名字，__file__指向该模块的导入文件名

与其类似的还有globals()和locals()函数，前者返回函数内能够访问的所有变量的命名，后者返回函数内所有能访问的全局变量的名字，并且两个函数都是字典，所以能够被keys()函数摘取

可以用reload()函数来重新导入已经导入的模块，有如：reload(module_name)，module_name是模块的名字，而非某个以字符串形式所表示的内容

python当中还有包的概念，包是某个分层的文件目录结构，其定义了一个由模块及子包和子包的子包所构成的python应用环境，还可以将其视为文件夹，但这个文件夹中必须存在python标识文件__init__.py

---

python文件的标准I/O有print（基本输出）、raw_input（键盘的字符输入）、input（键盘的表达式输入）

python当中可以用file对象来对文件进行打开或关闭操作，通常使用open()函数来对文件进行打开、创建或输入操作，有如：file object = open(file_name [, access_mode][, buffering])，后面的三个标识分为为需要访问的文件的字符串值，文件的打开方式（只读、写入、追加等等），用于设置寄存区的缓冲大小（0就没有，1的话buffering的值就取一，大于一则为寄存区的缓冲大小，如果取负值，则缓冲区大小为系统默认）

关闭则使用close()函数，刷新缓冲区并关闭文件，还有read()函数和write()函数分别用以控制文件读写

python中使用os模块对于文件进行更为细致的处理，同时file对象和os对象还提供了极多的对于文件对象的操作方法

当python脚本发生异常时需要对其进行捕获并且对其进行处理，使用try....except...else语句以捕捉异常

---

python的编写对于新人非常的友好，没有一些乱七八糟的标识符，省略了对于变量数据类型的指定，而且其会根据实际的变量类型来自动匹配其数据类型

包括数组（也就是列表）与元组，可以直接通过内存地址（即下标）进行访问，关键是不用指定数组内元素的数据类型

比起其它的程序语言python没有那么多条条框框

python可以被称作是一个万能的工具语言，包括着机器学习领域对其的高度依赖

---

Python内置函数：https://www.runoob.com/python/python-built-in-functions.html

Python-OS方法：https://www.runoob.com/python/os-file-methods.html

---



