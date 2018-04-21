---
layout: post
title:  "Ubuntu 16.04 install chrome"
date:   2018-4-21 19:49:53
categories: linux
description: install chrome for linux
keywords: chrome
author: wxcsdb88
---

*`Ubuntu 16.04`* 下使用 `apt` 安装 `Chrome` 的操作。

具体操作如下：

- 打开终端 *`terminal`*
- 将下载源加入到系统的源列表
`sudo wget http://www.linuxidc.com/files/repo/google-chrome.list -P /etc/apt/sources.list.d/`
- 导入谷歌软件的公钥
`wget -q -O - https://dl.google.com/linux/linux_signing_key.pub  | sudo apt-key add -`
- 更新源
`sudo apt-get update` (*切记需要在源更新完毕后才能执行下面的安装操作！*)
- 软件安装
`sudo apt-get install google-chrome-stable`
- 软件启动
`/usr/bin/google-chrome-stable`