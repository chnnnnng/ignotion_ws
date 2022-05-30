---
title: 
template: page
TOC: yes
---
[TOC]
## 安装环境

安装python3

```
sudo apt install python3-pip
pip --version
```

安装python3-venv

```
sudo apt-get install python3-venv
```

创建homeassistant系统用户和用户组

```
sudo useradd -r homeassistant
```

在/srv目录下创建homeassistant目录  

> /srv用于存放用户主动创建的、向外提供服务的文件

```
cd /srv
sudo mkdir homeassistant
```

更改此目录所有用户

```
sudo chown homeassistant:homeassistant homeassistant
```

切换至homeassistant用户
> 通过--shell（-s）参数，使用/bin/bash作为shell

```
sudo su -s /bin/bash homeassistant
```

创建虚拟环境

```
python3 -m venv homeassistant_venv
```

进入虚拟环境

```
source /srv/homeassistant/homeassistant_venv/bin/activate
```

## 安装依赖

```
pip install --upgrade pip
pip install netdisco
pip install warrant
```

## 安装依赖

```
pip install --upgrade pip
pip install netdisco
pip install warrant
```

## 开始安装

```
pip install homeassistant

#退出虚拟环境
exit
```

## 创建服务

为了方便使用systemctl工具管理homeassistant，下面创建一个service

```
cd /etc/systemd/system

sudo nano homeassistant.service
```

输入以下内容，并保存：

```
Description=Home Assistant
After=network.target

[Service]
Type=simple
User=homeassistant
Environment=PATH="$VIRTUAL_ENV/bin:$PATH"
ExecStart=/srv/homeassistant/homeassistant_venv/bin/hass -c "/home/homeassistant/.homeassistant"

[Install]
WantedBy=multi-user.target
```

接着更新系统设置

```
sudo systemctl daemon-reload
```

随后便可使用systemctl管理

```
#开启homeassistant
sudo systemctl start homeassistant.service

#关闭homeassistant
sudo systemctl stop homeassistant.service

#重启
sudo systemctl stop restart homeassistant.service

#查看状态（可以看报错信息）
systemctl status homeassistant

#将homeassistant设置为开机自启
sudo systemctl enable homeassistant.service

#禁用开机自启
sudo systemctl disable homeassistant.service
```

## 出错解决

通过`systemctl status homeassistant.service`发现几个报错：  
是关于`lru-dict`和`netifaces`这两个包缺失的问题。

解决办法:

切换至homeassistant用户

```
sudo su -s /bin/bash homeassistant
```

进入venv

```
source /srv/homeassistant/homeassistant_venv/bin/activate
```

安装缺失的包

```
pip install netifaces
pip install lru-dict
```

退出虚拟环境`exit`

重启homeassistant服务

```
sudo systemctl restart homeassistant.service
```

## 开放端口

使用ufw工具，打开8123端口

```
#查看当前端口状态
sudo ufw status

#开放8123端口
sudo ufw allow 8123

#使生效（重新开启防火墙）
sudo ufw enable

#可能需要reboot一下
sudo reboot

#最后可以用nmap确认一下是否已经开启
nmap 127.0.0.1 -p 8123
```

## 写在最后

经过以上步骤，HomeAssistant就安装成功了。  
在浏览器输入 http://此服务器ip:8123/ 即可进入HomeAssistant首次启动的配置页面。

> 首次启动需要时间，如果一时无法访问，可以稍等几分钟。

【开新坑】  
之后会记录一些HomeAssistant有趣的应用。