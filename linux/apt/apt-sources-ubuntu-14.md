---
layout: post
title:  "Ubuntu 14.04 trusty apt sources"
date:   2018-06-06 23:35:15
categories: apt linux
description: ubuntu 14.04 trusty apt sources config
keywords: apt, linux
author: wxcsdb88
---

*Ubuntu 14.04*, codename **trusty** apt sources list ref.

# apt sources for ubuntu 14.04

```bash
git clone https://github.com/wxcsdb88/awesome-config.git
cd awesome-config/linux/apt
mv /etc/apt/sources.list /etc/apt/sources.list-backup
cp sources.list.14  /etc/apt/sources.list
```

## aliyun

```text
deb http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse
```

## ubuntu

```text
deb http://archive.ubuntu.com/ubuntu/ trusty main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu/ trusty-security main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu/ trusty-updates main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu/ trusty-proposed main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu/ trusty-backports main restricted universe multiverse
deb-src http://archive.ubuntu.com/ubuntu/ trusty main restricted universe multiverse
deb-src http://archive.ubuntu.com/ubuntu/ trusty-security main restricted universe multiverse
deb-src http://archive.ubuntu.com/ubuntu/ trusty-updates main restricted universe multiverse
deb-src http://archive.ubuntu.com/ubuntu/ trusty-proposed main restricted universe multiverse
deb-src http://archive.ubuntu.com/ubuntu/ trusty-backports main restricted universe multiverse
```

## ustc

```text
deb https://mirrors.ustc.edu.cn/ubuntu/  trusty main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ trusty-security main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ trusty-updates main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ trusty-backports main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ trusty-proposed main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ trusty main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ trusty-security main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ trusty-updates main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ trusty-backports main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ trusty-proposed main restricted universe multiverse
```

## tsinghua

```text
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/  trusty main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ trusty-security main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ trusty-updates main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ trusty-backports main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ trusty-proposed main restricted universe multiverse
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ trusty main restricted universe multiverse
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ trusty-security main restricted universe multiverse
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ trusty-updates main restricted universe multiverse
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ trusty-backports main restricted universe multiverse
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ trusty-proposed main restricted universe multiverse
```

## sites

- [cn.ubuntu](http://cn.archive.ubuntu.com/ubuntu/)
- [ubuntu](http://archive.ubuntu.com/ubuntu/)
- [aliyun](http://mirrors.aliyun.com/ubuntu/)
- [ustc](https://mirrors.ustc.edu.cn/ubuntu)
- [tsinghua](http://mirrors.tuna.tsinghua.edu.cn/ubuntu/)
- [tw.ubuntu](http://tw.archive.ubuntu.com/ubuntu)
- [ftp.cuhk.edu.hk](http://ftp.cuhk.edu.hk/pub/Linux/ubuntu)