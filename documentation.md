---
title: Ignotion用户文档
template: page
TOC: enabled
---
[TOC]

## 开始之前

欢迎使用Ignotion。

Ignotion是一个简单易用的Markdown写作工具链，你可以使用Markdown语法撰写文章，通过Ignotion快速生成一系列漂亮的页面，并在本地或远程目录浏览它。

## 安装

正文正文正文正文正文正文正文正文正文  
正文正文正文正文正文正文正文正文正文

## 工作空间

工作空间是一个Ignotion博客的根目录，所有的文章、插图、主题、配置文件都存放在此。  
工作空间是一个包含配置文件config.yaml的普通目录  
一个标准的config.yaml文件如下:

```
#### Ignotion工作空间配置文件

### 站点信息
SITE_NAME: CHNG Ignotion
SITE_DESCRIPTION: An Easy-for-use Markdown Blog.
SITE_COPYRIGHT: Copyright ©2022 CHNG. 苏ICP备19058878号.

### 作者信息
AUTHOR_NAME: Chen.Y
AUTHOR_EMAIL: 596552206@qq.com
AUTHOR_INTRODUCTION: A student in Zhe Jiang University of Technology

### 本地目录设置
OUTPUT_DIR: HTML
RESOURCE_DIR: RES

### Ignotion主题
THEME: retro

### 远程目录设置
REMOTE_USER_AT_ADDR: root@chng.fun
REMOTE_WS: /root/ignotion_ws
REMOTE_PRIVATE_KEY: ./ignotion-chng-fun-mac
```

**SITE_NAME**、**SITE_DESCRIPTION**和**SITE_COPYRIGHT**  
分别是Ignotion生成网站的名称、描述及版权信息

**AUTHOR_NAME**、**AUTHOR_EMAIL**和**AUTHOR_INTRODUCTION**  
分别为作者姓名、邮箱和介绍信息

**OUTPUT_DIR**  
输出文件目录，该目录存放Ignotion生成的HTML文档及样式

**RESOURCE_DIR**  
资源文件目录，该目录存放Ignotion主题目录，以及用户的资源文件（如图片等）

**THEME**  
Ignotion主题, 位于 RESOURCE_DIR/theme/

**REMOTE_USER_AT_ADDR**  
远程SSH主机，22端口  
如：adam@yourhost

**REMOTE_WS**  
远程目录，本地的OUTPUT_DIR和RESOURCE_DIR将被上传至此处 
如：/home/adam/ignotion_ws

**REMOTE_PRIVATE_KEY**  
SSH私钥, 如：./my_private_key


## 目录

Ignotion的文章存放在目录中，工作空间是根目录。 
通过合理安排目录，你可以让你的文章**井然有序！**

一个目录具有三个名字，分别为：  

1. Directory name，即文件夹真实的名字
2. Display name, 即在文章或导航栏中显示的名字
3. Route name，即在URL中路由时使用的名字

要创建一个目录，请遵循以下步骤:  
1. 首先定位至工作空间  
2. 使用`mkdir`指令创建一个文件夹    
3. 接着进入该文件夹  
4. 使用`ignotion --make-dir`指令将该文件夹初始化为Ignotion目录  

该指令会要求用户输入Display name和Route Name，若留空，则将默认使用Directory Name。

```
$ cd ~/ignotion_ws
$ mkdir Articles
$ cd Articles
$ ignotion --make-dir
```

Ignotion目录初始化的本质是创建了一个名为.ignotion_dir的隐藏文件，你也可以手动创建该文件以初始化目录。

## 文章

要查看当前工作空间下所有的文章，只需执行：`ignotion -l`或`ignotion --list`  
该指令默认按时间顺序列出所有文章，若要以文件名顺序列出文章，请执行：`ignotion -l --name-order`  
要撰写一篇文章，只需执行以下几步：

1. 使用 `cd` 指令定位至文章目录。
2. 使用 `ignotion -n <文章名>` 指令创建新文章，该指令会在当前目录下创建一个符合模板要求的文章框架。
3. 使用你喜欢的编辑器编辑文章。

> `ignotion -n`指令可以接受更多参数：  
-n <文章名> 或 --new <文章名>  
--template <模板名>

> 注：指定文章名和模板名时，均不需要指名其后缀。  
如，要创建文件"三只小猪.md",只需执行`ignotion -n 三只小猪`

> 注：模板是一个html文件，位于主题目录下。  
用户也可以创建自己的模版文件。 

### Front Matter

Front Matter是Markdown文件上方以

```
---
---
```
划定的区域。

#### 标题

使用`title: `标签，可以指定文章的标题，使之区别于文件名。  
留空将使用文件名作为标题。

#### 模版

使用`template: `标签，可以为指定渲染模版。  
可选项：

- page
- empty

#### TOC

使用`TOC: `标签，可以指定是否显示TOC（Table of Content）。  
可选项：

- yes
- enable
- true

留空默认不使用TOC。  

> 注意  
TOC将以导航条的形式显示页面中，你也可以在文章中使用`[TOC]`标签引入TOC。


## 转译

“转译”也叫“生成”。撰写完成后，通过转译指令生成出HTML文件。 
要转译指定文章，请执行：

```
ignotion -t 要转译的文章.md
```

要转译所有文章，请执行

```
ignotion [-t | --translate] [all | a | -a | --all]
```

> TIPS：在任何时候，可以通过附加参数`--clear`来清空生成目录。如：`ignotion -ta --clear`将清空生成目录并转译所有文章。

## 远程目录与上载

转译完成后，可以在根目录下的生成目录（默认为HTML）中查看生成的HTML文档，也可以将生成目录上载至远程目录。

```
ignotion -u
```
将本地生成目录上载至远程目录。

> TIPS:  
转译和上载可以和作一句指令:`ignotion -ta -u`  
或`ignotion -ta -u --clear`

## Server

开启一个简易的WebServer。

```
ignotion --server 88
```