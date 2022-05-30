---
title: 
template: page
TOC: yes
---
## 引言

抽屉里正吃灰的树莓派4B已运行[Debian-Pi-Aarch64 2.0 ](https://gitee.com/openfans-community/Debian-Pi-Aarch64)一年有余，正逢近日学习ubuntu，故将系统重新刷至ubuntu-22.04-desktop-arm64+raspi.

## 系统安装

首先从ubuntu官网下载对应的[镜像](https://cn.ubuntu.com/download/raspberry-pi)。  
使用[树莓派镜像工具](https://www.raspberrypi.com/software/)将镜像下载至SD卡。  
插入CD卡，上电

如果有显示器以及键盘鼠标，可以直接进入桌面，开启ssh。  
如果没有，需要在**第一次**上电之前，在SD卡根目录下创建一个**名为ssh的空文件**。

```
# cd /Volume/system-boot
# touch ssh
```

## 喜闻乐见：换源

依然是换喜闻乐见的清华镜像源  

备份原来的源

```
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
```

写入新的源

```
sudo nano /etc/apt/sources.list
```

从[这里](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)复制，贴进去，保存。  

> 由于是arm架构，要将`http://mirrors.aliyun.com/ubuntu/`替换成`https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/`

```
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ jammy main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ jammy main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ jammy-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ jammy-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ jammy-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ jammy-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ jammy-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ jammy-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ jammy-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ jammy-proposed main restricted universe multiverse
```

最后，更新一下

```
sudo apt-get update
```

## 开启SSH

进入ubuntu.

```
# sudo apt-get update
# sudo apt-get install openssh-server
# sudo systemctl start ssh
# sudo systemctl enable ssh
```

允许root通过ssh登陆

```
sudo nano /etc/ssh/sshd_config
```

将

```
PermitRootLogin prohibit-password
```

改为

```
PermitRootLogin yes
```

保存退出，通过`sudo systemctl restart sshd`重启SSH服务


## 开启和关闭图形界面

关闭图形界面：

```
sudo systemctl set-default multi-user.target
sudo reboot
```

开启图形界面:

```
sudo systemctl set-default graphical.target
sudo reboot
```