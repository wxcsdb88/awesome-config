---
layout: post
title:  "Ubuntu 18.04 bionic apt sources"
date:   2018-06-07 00:05:15
categories: apt linux
description: ubuntu 18.04 apt bionic sources config
keywords: apt, linux
author: wxcsdb88
---

*Ubuntu 18.04*, codename **bionic** apt sources list ref.

# apt sources for ubuntu 18 bionic

```bash
git clone https://github.com/wxcsdb88/awesome-config.git
cd awesome-config/linux/apt
mv /etc/apt/sources.list /etc/apt/sources.list-backup
cp sources.list.18  /etc/apt/sources.list
```

## aliyun

```text
deb http://mirrors.aliyun.com/ubuntu/ bionic  main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic -security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic -updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic -proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic -backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic  main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic -security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic -updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic -proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic -backports main restricted universe multiverse
```

## ubuntu

```text
deb http://archive.ubuntu.com/ubuntu/ bionic  main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu/ bionic -security main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu/ bionic -updates main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu/ bionic -proposed main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu/ bionic -backports main restricted universe multiverse
deb-src http://archive.ubuntu.com/ubuntu/ bionic  main restricted universe multiverse
deb-src http://archive.ubuntu.com/ubuntu/ bionic -security main restricted universe multiverse
deb-src http://archive.ubuntu.com/ubuntu/ bionic -updates main restricted universe multiverse
deb-src http://archive.ubuntu.com/ubuntu/ bionic -proposed main restricted universe multiverse
deb-src http://archive.ubuntu.com/ubuntu/ bionic -backports main restricted universe multiverse
```

## ustc

```text
deb https://mirrors.ustc.edu.cn/ubuntu/  bionic  main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic -security main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic -updates main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic -backports main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic -proposed main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic  main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic -security main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic -updates main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic -backports main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic -proposed main restricted universe multiverse
```

## tsinghua

```text
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/  bionic  main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic -security main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic -updates main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic -backports main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic -proposed main restricted universe multiverse
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic  main restricted universe multiverse
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic -security main restricted universe multiverse
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic -updates main restricted universe multiverse
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic -backports main restricted universe multiverse
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic -proposed main restricted universe multiverse
```

## sites

- [cn.ubuntu](http://cn.archive.ubuntu.com/ubuntu/)
- [ubuntu](http://archive.ubuntu.com/ubuntu/)
- [aliyun](http://mirrors.aliyun.com/ubuntu/)
- [ustc](https://mirrors.ustc.edu.cn/ubuntu)
- [tsinghua](http://mirrors.tuna.tsinghua.edu.cn/ubuntu/)
- [tw.ubuntu](http://tw.archive.ubuntu.com/ubuntu)
- [ftp.cuhk.edu.hk](http://ftp.cuhk.edu.hk/pub/Linux/ubuntu)
