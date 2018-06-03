---
layout: post
title:  "Git 2F and multiple accounts config"
date:   2018-05-05 00:35:15
categories: git
description: git 2F and multiple accounts config
keywords: git, vcs, two-factor, 2F
author: wxcsdb88
---

*`git`* 双因子(素)认证(*two-factor authentication*)及多账号配置说明。

# 双因子认证

## 双因子(素)认证概念

一般来说，三种不同类型(独立不相干)的证据，可以证明一个人的身份。

1. 秘密信息：只有该用户知道、其他人不知道的某种信息，比如密码。
2. 个人物品：该用户的私人物品，比如身份证、钥匙。
3. 生理特征：该用户的遗传特征，比如指纹、相貌、虹膜等等。

这些证据就称为三种"因素"（factor）。因素越多，证明力就越强，身份就越可靠。

双因素认证就是指，通过认证同时需要两个因素的证据或使用两种独立不相干的证据来证明身份。

>银行卡就是最常见的双因素认证。用户必须同时提供银行卡和密码，才能取到现金。

依靠上述任何两种组合完成的认证，都可以称为是双因子认证。

由于目前网络应用最常用的单因子认证都是用户名和密码验证，因此网络应用要求的双因子验证都是配合用户名和密码验证方式的增强方式，也就是，上述*1+2*或者*1+3*模式。从应用上来看，*1+2*的模式更容易做系统迁移和维护。

## 双因子认证方案

### USB 令牌

智能卡和 USB KEY。事实上，两者的差别非常类似：某些智能卡可以支持USB接口；而且二者都是带微控制器，小的CHIP OS，还有安全存储区。当登录WEB服务的时候，必须插入 USB KEY，然后配合用户名和密码一齐提交服务器去认证。

### OTP 令牌

OTP 令牌是一个单独带数码液晶窗的小设备，通常带1个按钮，内部有可以支持设备正常工作1-2年的一个电池。OTP 令牌有伪随机数生成单元，在发行的时候做了时钟校对，之后，每10秒产生一个数字并且可以显示在数码 LCD 上。OTP 的意思是 *One Time Passwords*，很显然，这个密码用一次之后，下次就不会使用了。当登录WEB服务的时候，输入用户名和密码，还有这个 OTP 令牌的随机数一齐去获得认证。

### TOTP :fire:

TOTP 的全称是"基于时间的一次性密码"（**Time-based One-time Password**）。它是公认的可靠解决方案，已经写入国际标准 **`RFC6238`**。

步骤如下：

- 第一步，用户开启双因素认证后，服务器生成一个密钥。
- 第二步，服务器提示用户扫描二维码（或者使用其他方式），把密钥保存到用户的手机。也就是说，服务器和用户的手机，现在都有了同一把密钥。
  >注意，密钥必须跟手机绑定。一旦用户更换手机，就必须生成全新的密钥。
- 第三步，用户登录时，手机客户端使用这个密钥和当前时间戳，生成一个哈希，有效期默认为30秒。用户在有效期内，把这个哈希提交给服务器。
- 第四步，服务器也使用密钥和当前时间戳，生成一个哈希，跟用户提交的哈希比对。只要两者不一致，就拒绝登录。

TOTP 算法简介 :point_left:
>30秒期间都得到同一个哈希

```text
#TC = floor((unixtime(now) − unixtime(T0)) / TS)
TC = floor(unixtime(now) / 30)
TOTP = HASH(SecretKey, TC)
# default is SHA-1
```

>:key: **Google Authenticator** 是一个生成 TOTP 的手机 App

### 短信 OTP 令牌

短信 OTP 令牌是当用户登录 WEB 服务时，先输入用户名和密码，得到认证之后，服务器将会立即给预先登记的手机号码发一条带一次性 PIN 码的短信。用户收到之后，必须再输入这个短信PIN码来获得相应的使用权限。

### 码本

用户依据拥有的印刷的码本来回答WEB服务器的第二验证密码的问题。一种设计是，在 10X10 的格子里印有密码数字，用户根据登录页面提示的坐标去查看这个位置的密码数来输入第二验证密码。

### 生物特征认证

生物特征是属于被认证人生来具有的属性，因而是第三类的验证。能够用来作为认证的生物特征有指纹，声音，虹膜和脸部识别。近年来还有公司开发了静脉识别。生物特征认证的问题很多，有设别速度，识别率，设备成本等等。另外，和数字密码的可更改性比较，生物特征基本上对成人而言是终身的。

## 双因子认证优缺点

- 优点, 比单纯的密码登录安全得多。就算密码泄露，只要手机还在，账户就是安全的。各种密码破解方法，都对双因素认证无效。
- 缺点, 登录多了一步，费时且麻烦，用户会感到不耐烦。而且，它也不意味着账户的绝对安全，入侵者依然可以通过盗取 cookie 或 token，劫持整个对话（session）。

>*双因素认证还有一个最大的问题，那就是帐户的恢复。*

## git 双因子认证权限问题 :exclamation:

### 出现问题描述

>*github* 开启双因子认证后，执行*`git push`*出现以下问题

```bash
remote: Invalid username or password.
fatal: Authentication failed for 'https://github.com/...'
```

### 原因

在 GitHub 上采取双因子身份认证后，在 *`git push`* 的时候将会要求填写用户的用户名和密码，用户名就是用户在 GitHub 上申请的用户名，但是密码不是普通登录 GitHub 的密码。

### [解决方法](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line)

- ![根据链接地址生成`Personal access tokens`](resources/git-two-factor-add-access-token-full.png)
- ![本地`clone` 或 *提交代码时* 使用 *Personal access tokens* 替代密码](resources/git-two-factor-username-password.png)

>为了不每次都输入此 token ，可以设置记住 token :thumbsup:

```bash
git config --global credential.helper store
# git clone https://...
git push -u origin
# password:<Personal access tokens>
```

# git 多账号配置

## 同一网站(github.com)，配置多个账号

>假设已经存在一个默认的 *id_rsa* (默认的), 且已经配置账号 *wxcsdb88* 的 *SSH*

- 生成第二个账号的公钥

```bash
ssh-keygen -t rsa -C "your_email@youremail.com" -f ~/.ssh/second-username
#或 ssh-keygen -t rsa -C "your_email@youremail.com" 根据提示 输入生成文件名为 second-username
```

- 在 SSH 用户配置文件 `~/.ssh/config` 中指定对应服务所使用的公秘钥名称，如果没有 *config* 文件的话就新建一个，并输入以下内容

```bash
# Default github user(first@mail.com)
Host github.com
   User git
   Hostname github.com
   IdentityFile ~/.ssh/id_rsa
   # Port   ***

# second github user(second@mail.com)
Host futurever
   User git
   Hostname github.com
   IdentityFile ~/.ssh/second-username

``` 

- 测试是否能用各自账号正常访问网站

```bash
ssh -T git@github.com
# Hi wxcsdb88! You've successfully authenticated, but GitHub does not provide shell access.
ssh -T futurever
# Hi second-username! You've successfully authenticated, but GitHub does not provide shell access.
```

## 不同网站(github.com, oschina.cn)，多个账号

复制本机器`ssh-keygen` 生成的`pubkey` 到各网站账户 *[SSH配置位置](https://github.com/settings/keys)* 进行配置即可