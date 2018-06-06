---
layout: post
title:  "linux common alias"
date:   2018-06-03 22:30:53
categories: linux
description: linux common alias
keywords: config,linux
author: wxcsdb88
---

*linux* 下命令别名 `alias` 配置。

# why need

在linux系统中如果命令太长又不符合用户的习惯，那么我们可以为它指定一个别名。虽然可以为命令建立 “链接” 解决长文件名的问题，但对于带命令行参数的命令，链接就无能为力了。而指定别名则可以解决此类所有问题。

好处:

- 可以简化输入，节省时间，并提高效率。
> 定义的 alias 可以保存到 ~/.bashrc 文件中，以后在命令行中就可以直接使用了。
- 给危险的命令加上一个保险

>ex: `alias mv='mv -i'`, `alias rm='rm -i'`

# alias

用来设置指令的别名。

## 格式

> `alias [-p] [name[=value] ... ]`
> `alias 新的命令 ='原命令 -选项/参数'`

|编号|格式|说明|
|:--|:--|:--|
|1|`alias [-p]`|显示当前设置的别名|
|2|`alias name='command line'`|设置别名|
|3|`alias name`|显示指定的别名设置|
|4|`unalias name`|取消指定的别名设置|

## 配置

>使用命令 `type` `自定义命令名` ，查看自定义命令名是否被系统占用。

### 临时生效

直接在 *shell* 里设定的命令别名，在终端关闭或者系统重新启动后都会失效。

### 永久生效

- 当前用户
> 在当前用户下的 `.profile`, `.bashrc`, `.bash_aliases` 其中一个文件中配置 `alias`，若是没有这些文件可以自己新建一个。
- 所有用户
> 修改 `/etc` 目录下的 `profile`, `bashrc`, `profile.d/*` 文件就可以了。在CentOS7下，这个文件是`/etc/bash.bashrc`。

### 修改立即生效

`source .bashrc` 或者 `. .bashrc` 命令使修改立即生效。

### 配置文件加载顺序

**ubuntu 18.04** 配置文件加载顺序 `/etc/profile`, `/etc/bash.bashrc`, `/etc/profile.d/*`,  `$HOME/.profile`, `$HOME/.bashrc`, `$HOME/.bashrc_alias`

# 命令

## 常用

```bash
alias cp='cp -i'
alias l.='ls -d .* --color=tty'
#alias l.='ls -d .* --color=auto'
alias ll='ls -l --color=tty'
#alias ll='ls -l --color=auto'
alias ls='ls --color=tty'
#alias ls='ls --color=auto'
alias mv='mv -i'
alias rm='rm -i'
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'
```

## 模拟DOS风格的命令

```bash
alias clr=clear
alias cls=clear
alias copy='cp -i'
alias del='rm -i'
alias delete='rm -i'
alias dir='ls -alg'
alias home='cd ~'
alias ls='ls -F'
alias md=mkdir
alias move='mv -i'
alias type=more

alias cd..='cd ..'
alias home='cd /home/dave/public_html'

alias list='ls -la'
```

## other

```bash
alias cp='cp -i'
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
alias grep='grep --color=auto'

alias attrib='chmod'
alias chdir='cd'
alias copy='cp'
alias d='dir'
alias del='rm'
alias deltree='rm -r'
alias dir='/bin/ls $LS_OPTIONS --format=vertical'
alias edit='pico'
alias ff='whereis'
alias ls='/bin/ls $LS_OPTIONS'
alias mem='top'
alias move='mv'
alias pico='pico -w -z'
alias search='grep'
alias v='vdir'
alias vdir='/bin/ls $LS_OPTIONS --format=long'
alias which='type -path'
alias wtf='watch -n 1 w -hs'
alias wth='ps -uxa | more'
```