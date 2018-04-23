---
layout: post
title:  "Gitlab install and config with docker"
date:   2018-04-23 23:27:15
categories: git, tools
description: gitlab install and config with docker
keywords: git, vcs, gitlab
author: wxcsdb88
---

*`CentOS`* 下使用 `docker`及`docker-compose`安装代码版本管理工具 `gitlab` 并进行代码本地远程备份配置。

# 介绍

*`Gitlab`* 是一个用`Ruby on Rails`开发的开源项目管理程序，可以通过`WEB`界面进行访问公开的或者私人项目。它和`Github`有类似的功能，能够浏览源代码，管理缺陷和注释。

# 软件安装

## yum 镜像设置
[仓库地址修改](https://www.cnblogs.com/renpingsheng/p/7845096.html)

```bash
yum clean all
yum makecache
```

## 旧版本 docker 及依赖卸载

```bash
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine
```

## [docker 安装](https://docs.docker.com/install/linux/docker-ce/centos/#install-using-the-repository)

#### 依赖安装

```bash
sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
```

### docker 源设置

```bash
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

### docker 版本查看及安装

```bash
# 版本查看
yum list docker-ce --showduplicates | sort -r

# 安装
sudo yum install docker-ce
#sudo yum install <FULLY-QUALIFIED-PACKAGE-NAME>

# 启动
sudo systemctl start docker
```

### docker 其他配置

```bash
# 非 root 用户运行
sudo groupadd docker
# gpasswd -a user group
# usermod -aG group user 
sudo usermod -aG docker $USER
#gpasswd -d user group 

# start on boot
# systemd
sudo systemctl enable docker
#sudo reboot
```

## docker-compose 下载

```bash
# v1.19.0
sudo curl -L https://github.com/docker/compose/releases/download/1.19.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

# 安装完成后，查看是否成功
docker-compose -v
# docker-compose version 1.19.0, build 9e633ef
```

## gitlab 相关数据目录准备

>mkdir /data/docker/gitlab
容器对应挂载目录

```bash
/data/docker/gitlab/redis:/var/lib/redis:Z
/data/docker/gitlab/postgresql:/var/lib/postgresql:Z
/data/docker/gitlab/gitlab:/home/git/data:Z

#gitlab 默认root 5iveL!fe
```

## gitlab 相关镜像下载

### docker-compose 方式创建

[仓库地址](https://github.com/wxcsdb88/docker-gitlab.git) 请选择 **`v10.5.1`** 及以上版本

# gitlab 安装及初始化(旧数据恢复)

```bash
# 首次创建(备份)，看是否成功！
#docker-compose -f ${compose_file} run --rm gitlab app:rake gitlab:backup:create
docker-compose  run --rm gitlab app:rake gitlab:backup:create
# 成功的话，尝试启动服务
docker-compose up -d
```

>列出可恢复版本

```bash
docker-compose run --rm gitlab app:rake gitlab:backup:restore
 #列出可用备份版本
```

>指定恢复版本

```bash
#如果是其他服务器copy的请copy至相应备份目录后操作！
docker-compose run --rm gitlab app:rake gitlab:backup:restore BACKUP=1521042630_2018_03_14_10.5.1
# 指定恢复到版本1521042630
#1521042630_2018_03_14_10.5.1_gitlab_backup.tar
```

# expect 相关工具安装

```bash
#sudo yum install expect
sudo yum install tcl tk expect
```

# gitlab master 相关脚本

需要隔3小时备份一次，一天备份9个，备份5天的
>定时备份脚本
cd ~/gitlab
gitlab-auto-backup.sh

```bash
#! /bin/sh
# This script run each hours
compose_file='/home/futurever/gitlab/docker-compose.yml'
docker-compose -f ${compose_file} run --rm gitlab app:rake gitlab:backup:create
```

>定时远程备份脚本
三小时备份一次，间隔远程备份时间应该小于3小时，防止服务器宕机缺失备份！
120 分!
gitlab-expect-scp.sh

```bash
#！/bin/bash
delete_days=5
minutes=120
src_dir='/data/docker/gitlab/gitlab/backups'
remote_server='futurever@110.114.115.119'
remote_backup_dir='~/gitlab/backups'
cd ${src_dir}
need_copy_backup_count=`find . -type f -name '*.tar' -mmin -${minutes}|wc -l`
if [[ ${need_copy_backup_count} -gt 0 ]]; then
       echo "${need_copy_backup_count} files need scp"
       expect -c "
set timeout 1800; ##设置拷贝的时间，根据目录大小决定
spawn /usr/bin/scp `find . -type f -name '*.tar' -mmin -${minutes} |xargs` ${remote_server}:${remote_backup_dir}
expect {
\"*yes/no*\" {send \"yes\r\"; exp_continue}
\"*password*\" {send \"123456#\r\";} ##远程IP的密码。
}
expect eof;"
fi
need_delete_backup_count=`find . -type f -name '*.tar' -mtime +${delete_days}|wc -l`
if [[ ${need_delete_backup_count} -gt 0 ]]; then
 echo "delete the ${delete_days} days ago files, count is ${need_delete_backup_count}"
 # delete files
 find . -type f -name '*.tar' -mtime +${delete_days} -exec rm -f {} \;
fi

```

>gitlab master 定时任务

```bash
# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
#
# For more information see the manual pages of crontab(5) and cron(8)
#
# m h dom mon dow command
  0 */3   * * *  bash /home/futurever/gitlab/gitlab-auto-backup.sh
  5 */3   * * *  bash /home/futurever/gitlab/gitlab-expect-scp.sh

```

# gitlab slave 相关脚本

>gitlab-auto-delete.sh

```bash
#！/bin/bash
delete_days=7
keep_file_count=49
backup_dir='~/futurever/gitlab/backups'
cd ${backup_dir}
backup_file_count=`find . -type f -name '*.tar'|wc -l`
if [[ ${backup_file_count} -ge ${keep_file_count} ]]; then
     echo "total backup files is ${backup_file_count} >= ${keep_file_count} can delete files before ${delete_days} days ago!"
     find . -type f -name '*.tar' -mtime +${delete_days} -exec rm -f {} \;
else
    echo "total backup files is ${backup_file_count} < least backup file numbers ${keep_file_count}, no delete!"
fi
```

>gitlab slave  定时任务
crontab -e

```bash
# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
#
# For more information see the manual pages of crontab(5) and cron(8)
#
# m h dom mon dow command
 0 */3 * * * bash /home/futurever/gitlab/gitlab-auto-delete.sh
```

# 额外安装

```bash
htop nmap
```

>定时任务及开机启动配置

```bash
/sbin/service crond start
/sbin/service crond stop
/sbin/service crond restart
/sbin/service crond reload
以上1-4行分别为启动、停止、重启服务和重新加载配置。

要把cron设为在开机的时候自动启动，在 /etc/rc.d/rc.local 脚本中加入 /sbin/service crond start 即可
```

# 重启自动启动gitlab服务

```bash
docker-compose -f /home/futurever/gitlab/docker-compose.yml up -d
```

# 端口设置

>开放端口查看 nmap 127.0.0.1
netstat -lnpt

```bash
97:22 #https
99:80 # http

#smtp 25 465
#imap 993
```

# 自动备份失效

```bash
root用户 不能访问到定时任务命令 /usr/local/bin/docker-compose ，直接写上全路径，进行备份！
```