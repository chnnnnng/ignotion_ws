---
title: Ignotion指令集合
template: page
TOC: yes
---
## 工作空间

##### 初始化工作空间：`ignotion --init-ws`

## 目录

##### 初始化目录：`ignotion --make-dir`

## 文章

##### 列出所有文章

`--list(-l)` 按时间顺序列出工作空间下所有文章

`--name-order` 附加项，按名称排序

##### 创建新文章

`--new(-n) NAME` 创建名为NAME的文章，文件名为NAME.md  
🌰   
ignotion -n helloworld  
ignotion -n article/helloworld

`--template TEMPLATE_NAME` 附加项，使用指定的模板创建  
🌰  
ignotion -n helloworld --template page

## 转译

`--translate(-t) FILENAME.md` 转译名为FILENAME.md的文章（无需指明所在目录）  
🌰  
ignotion -t helloworld.md

`--translate(-t) all(a|-a|-all)` 转译工作空间下所有文章  
🌰  
ignotion -ta

`--clear` 附加项，清除生成目录  
🌰  
ignotion -ta --clear

## 远程目录与上载

`--upload(-u)` 上载至远程目录  
🌰  
ignotion -ta -u

## Server

`--server PORT` 在PORT端口开启一个简易Web服务器。  
🌰  
ignotion --server 88
