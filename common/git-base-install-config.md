---
layout: post
title:  "Git install and config"
date:   2018-04-22 17:42:15
categories: git
description: git install and config
keywords: git, vcs
author: wxcsdb88
---

*`windows`*,*`linux`* 及 *`mac`* 下安装代码版本管理工具 `git`并进行简单配置。

# 介绍

Git是一个免费的开源分布式版本控制系统，可以有效、高速的处理从很小到非常大的项目版本管理。Git是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。

## 特点

- git和其他版本控制系统（如CVS）有不少的差别，git本身关心文件的整体性是否有改变，但多数的版本控制系统如CVS或Subversion系统则在乎文件内容的差异。git拒绝保持每个文件的版本修订关系。因此查看一个文件的历史需要遍历各个history快照；git隐式处理文件更名，即同名文件默认为其前身，如果没有同名文件则在前一个版本中搜索具有类似内容的文件。
- git更像一个文件系统，直接在本机上获取数据，不必连接到主机端获取数据。 每个开发者都可有全部开发历史的本地副本，changes从这种本地repository复制给其他开发者。这些changes作为新增的开发分支被导入，可以与本地开发分支合并。
- 分支是非常轻量级的，一个分支仅是对一个commit的引用。

## 库目录

```text
hooks：存储钩子的文件夹
logs：存储日志的文件夹
refs：存储指向各个分支的指针（SHA-1标识）文件
objects：存放git对象
config：存放各种设置文档
HEAD：指向当前所在分支的指针文件路径，一般指向refs下的某文件
```

## 数据结构

Git有两种数据结构：可变的索引（index或stage或cache)用于缓冲工作目录信息与下一次提交的版本信息；不变的、仅追加的对象数据库。
对象数据库包含4类对象：

- blob (二进制大对象)是一个文件的内容。Blobs没有适当的文件名、时间戳、或其他元数据。一个blob的内部名字是它的内容的hash。
- tree对象等效于目录。包含文件名列表以及文件的类型比特、到blob或tree对象的引用。tree对象是源树(source tree)的快照。用默克树实现。
- commit对象链接tree对象在一起而成为history. 包含顶层源目录的tree对象名字、一个时间戳、log信息、0个或多个父commit对象的名字。
- tag对象是一个容器，包含了到另一个对象的引用，也可以增加关于另外对象的元数据。通常它保存需要追溯的特定版本数据的一个commit对象的数字签名。

每个对象用其内容的SHA-1 hash来标识。对象放入它的hash值得前两个字符标识的目录中，其余hash字符作为这个对象的文件名。
Git数据库中不变引用的对象将会被垃圾回收清除。Git命令可以创建、移动、删除引用。"git show-ref"列出所有引用。某些引用类型：

- heads: 引用一个本地对象，是commit的指针。每个head可以指任意一个这样的指针。可以包含任意数量的heads。而"HEAD"（全部大写），仅仅指的是当前有效的head。默认情况下，在每个仓库下都有一个head，叫做- master。
- remotes: 引用远程repository中的一个对象
- stash: 引用一个还没有committed的一个对象
- meta: 例如一个bare repository中的一个配置, 用户权限; refs/meta/config名字空间等
- tags:

# [git安装](https://git-scm.com)

>请根据你当前所使用系统版本，选择合适的版本下载。

## windows

直接下载*windows版git*安装即可

## linux

你可以选择使用*apt*或*源码下载*方式安装*git*
>*apt* 方式 `sudo apt-get install git`

## mac

`sudo brew install git`

# git 配置

## 全局账号配置

```shell
git config --global user.email email
git config --global user.name nickname
git config -l
```

## ssh key 生成

```shell
ssh-keygen -t rsa -b 4096 -C "youremail@xx.xx"
```

>如果你需要配置多个账号的ssh key，可以在保存时选择不同文件名存储

## beautiful log 格式配置

```shell
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

# tips

- 如果是私有仓库或者需要登录才能*clone*的项目，可以配置`ssh-key`,并使用*ssh*方式*clone*项目，这样无需输入密码
- 默认项目的保护分支为`master`, 如需要强制提交更新覆盖代码(不推荐)，需要去除保护并进行相应设置
- [git 相关命令参考](https://git-scm.com/docs)