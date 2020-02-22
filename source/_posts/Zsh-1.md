---
title: Zsh-1
date: 2020-02-21 22:35:07
tags: [GNU/Linux,随笔]
categories: 软件
---

## Shell-Zsh

### oh my zsh

* 配置过程

**相关指令:**

* 查看系统当前使用的shell
> `$ echo $SHELL`
---
* 查看系统支持Shell列表
> `$ cat /etc/shells`
---
* 安装zsh
> `apt-get -y install zsh`
---
* 切换shell为zsh
> `$ chsh -s /bin/zsh`
---
* 修改主题
> `$ vim ~/.zshrc`
---
* 这里将`ZSH_THEME`改成ys
> `ZSH_THEME="ys"`
--
* 更新配置
> `$ source ~/.zshrc `
---

**补全插件配置:**

* incr.zsh补全插件下载
> `$ wget http://mimosa-pudica.net/src/incr-0.2.zsh`

* 将此插件放到oh-my-zsh目录的插件库下:
```
$cd ~/.oh-my-zsh/plugins/incr
$mkdir incr
# root @ debian in ~/.oh-my-zsh/plugins/incr on git:master x [15:05:07] 
$ ls
incr-0.2.zsh
```

* 在~/.zshrc文件末尾加上
> `emacs ~/.zshrc`
> `source ~/.oh-my-zsh/plugins/incr/incr*.zsh`

* 更新配置:
> `$ source ~/.zshrc`

---

**与vim的提示冲突的解决方法:**

* 使用自动补全插件可能会与vim的提示功能相冲突，如会报以下错误:

```
$ vim t
_arguments:451: _vim_files: function definition file not found
```
---
* 解决方法：将`~/.zcompdump*`删除即可
```
$ rm -rf ~/.zcompdump*
$ exec zsh
```

---

**获取方式(Git/Curl/Wget):**

* Git拉取并安装
> `wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh`

* Curl
> `sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"`

* Wget
> `sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"`

* Git源码地址[跳转](https://github.com/ohmyzsh/ohmyzsh)
> `https://github.com/ohmyzsh/ohmyzsh`

* Zsh主题乐园[跳转](http://blog.ysmood.org/my-ys-terminal-theme/)
> `http://blog.ysmood.org/my-ys-terminal-theme/`

---

**参考资料(技术博客):**

* 修改Linux的shell从默认的bash切换为zsh[跳转](http://www.findme.wang/blog/detail/id/282.html)
> `http://www.findme.wang/blog/detail/id/282.html`

* oh-my-zsh,让你的终端从未这么爽过[跳转](https://www.jianshu.com/p/d194d29e488c)
> `https://www.jianshu.com/p/d194d29e488c`

* 写给 Pythonist 的 Spacemacs 入门指北[跳转](https://www.jianshu.com/p/c5cc672aae63)
> `https://www.jianshu.com/p/c5cc672aae63`

* oh-my-zsh,最好用的shell,没有之一[跳转](https://www.itshutong.com/articles/281/oh-my-zsh-the-best-shell-none)
> `https://www.itshutong.com/articles/281/oh-my-zsh-the-best-shell-none`

---

**其它内容:**

* Shell[跳转]()
> 本篇
> `oh my zsh`

* 编辑器[跳转](http://unit-serow.com/2020/02/21/Emacs-1/#more)
> `spacemacs`

* X window[跳转](http://unit-serow.com/2020/02/20/Window-1/#more)
> `X.org/GNOME`

---
