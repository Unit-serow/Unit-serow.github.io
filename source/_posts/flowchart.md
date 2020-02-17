---
title: makedown流程图-flowchart
date: 2020-02-05 13:15:51
tags: 杂项
categories: 软件
---

### 语法结构

**概述:**
* 流程图的语法大概可以分为两部分:定义元素与连接元素
* 定义变量所使用的语句大概结构是X=Y: Z
* X是变量名，Y是操作模块名，Z是具体显示的文字内容，注意冒号后的空格，有空格的时候才能被识别

**基本语法:**

* 由于渲染的问题，这里用`<.>`代替

```
···flow
tag=>type: content:>url
...
```

```
...
tag1(...)->tag2(...)->tag3(...)
···
```

* 括号内语句用逗号分隔

**定义元素语法:**
* `tag=>type: content:>url`
* tag：标签，用于连接元素时使用
* type：该标签的类型，共有6种类型如下
* content：流程语句中放置的内容 
* type:与content之间有一个空格
* url：链接，与流程语句绑定

**连接元素语法:**
* 使用->符号，->表示下一步要执行的操作：
* `st->in->op->cond`
* 表示的是先从st转到in，然后再到op，最后到cond
* 可以连续写，也可以分开写

**判断分支语法:**
* condition是判断，可以取yes和no两种结果，对于不同结果可以有不同走向
* `cond(yes)->out`表示condition成立时转向out执行
* `cond(no)->op`表示condition不成立时转向op执行

**操作模块说明:**
操作模块一共有以下六种:

|操作模块名|表示含义说明|
|:----|:----|
|start|开始|
|end|结束|
|operation|普通操作块|
|subroutine|子任务块|
|condition|判断块|
|inputoutput|输入输出块|

---

**示例说明-1:**
竖向:
```
···flow
st=>start: 开始框
op=>operation: 处理框
cond=>condition: 判断框(是或否?)
sub1=>subroutine: 子流程
io=>inputoutput: 输入输出框
e=>end: 结束框

st->op->cond
cond(yes)->io->e
cond(no)->sub1(right)->op
···
```

```flow
st=>start: 开始框
op=>operation: 处理框
cond=>condition: 判断框(是或否?)
sub1=>subroutine: 子流程
io=>inputoutput: 输入输出框
e=>end: 结束框

st->op->cond
cond(yes)->io->e
cond(no)->sub1(right)->op
```

---

示例说明-2:
横向:
```
···flow
st=>start: 开始框
op=>operation: 处理框
cond=>condition: 判断框(是或否?)
sub1=>subroutine: 子流程
io=>inputoutput: 输入输出框
e=>end: 结束框

st(right)->op(right)->cond
cond(yes)->io(bottom)->e
cond(no)->sub1(right)->op
···
```

```flow
st=>start: 开始框
op=>operation: 处理框
cond=>condition: 判断框(是或否?)
sub1=>subroutine: 子流程
io=>inputoutput: 输入输出框
e=>end: 结束框

st(right)->op(right)->cond
cond(yes)->io(bottom)->e
cond(no)->sub1(right)->op
```

---

实例说明-3:
```
···flow   
st=>start: 开始语句
in=>inputoutput: 输入值
e=>end: 结束语句
op=>operation: 执行操作
cond=>condition: 是否成立？
out=>inputoutput: 输出值

st->in->op->cond
cond(yes)->out
cond(no)->op
out->e
···
```

```flow   
st=>start: 开始语句
in=>inputoutput: 输入值
e=>end: 结束语句
op=>operation: 执行操作
cond=>condition: 是否成立？
out=>inputoutput: 输出值

st->in->op->cond
cond(yes)->out
cond(no)->op
out->e
```

---

示例说明-4:
```
···flow
st=>start: Start
e=>end: Why are you worried?
cond1=>condition: Do you have a problem?
cond2=>condition: Can you solve it?
op=>operation: Since you can't solve it,

st->cond1
cond1(yes)->cond2
cond1(no)->e
cond2(yes)->e
cond2(no)->op->e
···
```

```flow
st=>start: Start
e=>end: Why are you worried?
cond1=>condition: Do you have a problem?
cond2=>condition: Can you solve it?
op=>operation: Since you can't solve it,

st->cond1
cond1(yes)->cond2
cond1(no)->e
cond2(yes)->e
cond2(no)->op->e
```

---

**示例说明-5:**
```
···flow
st=>start: Start|past:>http://www.baidu.com
e=>end: End:>http://www.baidu.com
op1=>operation: My Operation|past
op2=>operation: Stuff|current
sub1=>subroutine: My Subroutine|invalid
cond=>condition: Yes or No?|approved:>http://www.baidu.com
c2=>condition: Good idea|rejected
io=>inputoutput: catch something...|request

st->op1(right)->cond
cond(yes, right)->c2
cond(no)->sub1(left)->op1
c2(yes)->io->e
c2(no)->op2->e
···
```

```flow
st=>start: Start|past:>http://www.baidu.com
e=>end: End:>http://www.baidu.com
op1=>operation: My Operation|past
op2=>operation: Stuff|current
sub1=>subroutine: My Subroutine|invalid
cond=>condition: Yes or No?|approved:>http://www.baidu.com
c2=>condition: Good idea|rejected
io=>inputoutput: catch something...|request

st->op1(right)->cond
cond(yes, right)->c2
cond(no)->sub1(left)->op1
c2(yes)->io->e
c2(no)->op2->e
```

---

参考资料:

参考资料:[跳转](http://flowchart.js.org/)
`http://flowchart.js.org/`

获取方式:
`npm install --save hexo-filter-flowchart`

配置方式：
安装完成后进入根目录修改配置文件
```
flowchart: 
#raphael:#optional, the source url of raphael.js 
#flowchart:#optional, the source url of flowchart.js
options:#options used for `drawSVG`
```
