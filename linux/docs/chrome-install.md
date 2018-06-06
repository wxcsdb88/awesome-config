---
layout: post
title:  "Ubuntu 16.04+ install chrome"
date:   2018-04-21 19:49:53
categories: linux
description: install chrome for linux
keywords: chrome,tools
author: wxcsdb88
---

*`Ubuntu 16.04+`* 下使用 `apt` 安装 `Chrome` 的操作。

具体操作如下：

- 打开终端 *`terminal`*
- 将下载源加入到系统的源列表
> `sudo wget http://www.linuxidc.com/files/repo/google-chrome.list -P /etc/apt/sources.list.d/`
- 导入谷歌软件的公钥
> `wget -q -O - https://dl.google.com/linux/linux_signing_key.pub  | sudo apt-key add -`
- 更新源
> `sudo apt-get update` (*切记需要在源更新完毕后才能执行下面的安装操作！*)
- 软件安装
> `sudo apt-get install google-chrome-stable`
- 软件启动
> `/usr/bin/google-chrome-stable`

# 错误及解决

> ubuntu 18.04 (root 用户)
> [2541:2541:0603/134644.803948:ERROR:zygote_host_impl_linux.cc(88)] Running as root without --no-sandbox is not supported. See https://crbug.com/638180.

## 以 root 用户启动

```bash
/usr/bin/google-chrome-stable --no-sandbox
```

## 修改权限

```bash
sudo chown $USER:root /usr/bin/google-chrome-stable
# 找到当前用户下google-chrome 同样修改权限，以当前用户启动即可
# sudo chown -R $USER ~/.config/usr/bin/google-chrome-stable
```