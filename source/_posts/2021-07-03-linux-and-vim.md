---
title: linux-and-vim
auther: yuquan
reward: false
date: 2021-07-03 17:31:02
tags: vim
categories: vim
---

# linux下的vim的使用

![](https://s2.loli.net/2022/06/16/ETAtCkNbVOfsnhr.png)



<!--more-->

## 1、zsh终端的安装和使用

**安装：**

`sudo apt install zsh`

**安装[oh-my-zsh](https://ohmyz.sh/)**

`sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`

或者

`sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"`

**配置文件：**

`vim ./zshrc`可以在ZSH_THEME="ys"配置相应的主题，在官网上可以找到相应的主题。然后终端执行`source ~/.zshrc`

oh-my-zsh 的自带插件都储存在~/.oh-my-zsh/plugins目录中，如果你希望安装一个插件，可以在 ~/.zshrc的 plugins=(xxx, xxx, ...) 这一行里加入插件名称.

如果你需要安装第三方插件和主题，你可以在 "~/.zshrc" 的某一行（比如末尾）加入 source /path/to/plugin,根据自己的插件输入目录。

## 2、vim插件[vim-plug](https://github.com/junegunn/vim-plug)的安装和使用

**安装：**

`mkdir -p  ~/.vim/autoload/`

`cp plug.vim  ~/.vim/autoload/plug.vim`

**插件的添加和使用：**
编辑~/.vimrc文件中的内容，比如安装“lightline.vim” 插件

```bash
call plug#begin('~/.vim/plugged')
Plug 'itchyny/lightline.vim'
call plug#end()
```

**运行命令重新加载：**

`:source ~/.vimrc`

插件的安装和卸载：

> ```bash
> 打开 vim 使用命令 :
> :PlugInstall
> 你也可以使用以下命令，指定安装特定的插件：
> :PlugInstall gist-vim 
> 打开 vim 使用命令卸载：
> :PlugClean
> ```

**更新插件：**

使用以下命令，可以更新vim-plug插件自身：

`:PlugUpgrade`

使用以下命令，可以批量更新所有已安装的插件：

`:PlugUpdate`

使用以下命令，可以查看当前已安装插件的状态信息：

`:PlugStatus`

[Vim常用的插件推荐](https://zhuanlan.zhihu.com/p/84954261)

**Vim操作的使用：**

1、Vim键盘

![](https://s2.loli.net/2022/06/16/A73MBZCnXVQ4Gms.gif)

2、Vim命令图解

![](https://s2.loli.net/2022/06/16/8trbwD5AJq4aT3u.png)

3、Vim使用

![](https://s2.loli.net/2022/06/16/6jXo4qcvLyJsViQ.png)

![](https://s2.loli.net/2022/06/16/xeGgW75fuwvD3PN.png)

## 3、Tmux的安装和使用

==**介绍：**==

![](https://s2.loli.net/2022/06/16/ETAtCkNbVOfsnhr.png)

tmux 是一款优秀的终端复用工具（terminal multiplexer），是常用的开发工具，使用它最直观的好处就是，通过一个终端登录远程主机并运行tmux后，在其中可以开启多个控制台而无需再“浪费”多余的终端来连接这台远程主机。[使用手册](http://louiszhai.github.io/2017/09/30/tmux/#%E5%9F%BA%E6%9C%AC%E6%A6%82%E5%BF%B5)

==**关于会话，窗口，进程:**==

命令行的典型使用方式是，打开一个终端窗口（terminal window，以下简称 “窗口”），在里面输入命令。 用户与计算机的这种临时的交互，称为一次 “会话”（session） 。

会话的一个重要特点是，窗口与其中启动的进程是连在一起的。打开窗口，会话开始；关闭窗口，会话结束，会话内部的进程也会随之终止，不管有没有运行完。

一个典型的例子就是，SSH 登录远程计算机，打开一个远程窗口执行命令。这时，网络突然断线，再次登录的时候，是找不回上一次执行的命令的。因为上一次 SSH 会话已经终止了，里面的进程也随之消失了。

为了解决这个问题，会话与窗口可以 “解绑”：窗口关闭时，会话并不终止，而是继续运行，等到以后需要的时候，再让会话 “绑定” 其他窗口。

tmux 就是会话与窗口的 “解绑” 工具，将它们彻底分离。

（1）它允许在单个窗口中，同时访问多个会话。这对于同时运行多个命令行程序很有用。

（2）它可以让新窗口 “接入” 已经存在的会话。

（3）它允许每个会话有多个连接窗口，因此可以多人实时共享会话。

（4）它还支持窗口任意的垂直和水平拆分。

类似的终端复用器还有 GNU Screen。tmux 与它功能相似，但是更易用，也更强大。

![](https://s2.loli.net/2022/06/16/EQpy5B6zO7YcMvj.jpg)

==**tmux概念**==

使用 Tmux 的时候不用去背指令，所有的指令都可以在 `.tmux.conf` 配置文件中绑定自己顺手的快捷键，也可以配置开启鼠标。

在Tmux逻辑中，需要分清楚Server > Session > Window > Pane这个大小和层级顺序是极其重要的，直接关系到工作效率：

- Server：是整个tmux的后台服务。有时候更改配置不生效，就要使用tmux kill-server来重启tmux。
- Session：是tmux的所有会话。我之前就错把这个session当成窗口用，造成了很多不便里。一般只要保存一个session就足够了。
- Window：相当于一个工作区，包含很多分屏，可以针对每种任务分一个Window。如下载一个Window，编程一个window。
- Pane：是在Window里面的小分屏。最常用也最好用

了解了这个逻辑后，整个Tmux的使用和配置也就清晰了。

![](https://s2.loli.net/2022/06/16/fJ2XCRnSlTEqZuN.png)

[详细的使用书籍](https://pityonline.gitbooks.io/tmux-productive-mouse-free-development_zh/content/index.html)

[使用操作](https://www.freeaihub.com/article/tmux.html)


## 4、linux快捷键使用

**快捷键：**

![](https://s2.loli.net/2022/06/16/1k6HhzGNZd3YQ5E.jpg)

![](https://s2.loli.net/2022/06/16/9vJuMwGEkLjWN3Q.png)
