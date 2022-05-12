---
TOC: enabled
---
[TOC]

## 开始之前

欢迎使用Ignotion。

开始之前，请允许[我](https://chng.fun/)介绍一下Ignotion为何物.

Ignotion是一个简单易用的Blog工具，你可以使用markdown语法撰写文章，之后通过Ignotion快速生成一个漂亮的HTML网页，并方便的部署在远程目录上。

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

> **SITE_NAME**、**SITE_DESCRIPTION**和**SITE_COPYRIGHT**  
分别是Ignotion生成网站的名称、描述及版权信息

> **AUTHOR_NAME**、**AUTHOR_EMAIL**和**AUTHOR_INTRODUCTION**  
分别为作者姓名、邮箱和介绍信息

> **OUTPUT_DIR**  
输出文件目录，该目录存放Ignotion生成的HTML文档及样式

> **RESOURCE_DIR**  
资源文件目录，该目录存放Ignotion主题目录，以及用户的资源文件（如图片等）

> **THEME**  
Ignotion主题, 位于 RESOURCE_DIR/theme/

> **REMOTE_USER_AT_ADDR**  
远程SSH主机，22端口  
如：adam@yourhost

> **REMOTE_WS**  
远程目录，本地的OUTPUT_DIR和RESOURCE_DIR将被上传至此处 
如：/home/adam/ignotion_ws

> **REMOTE_PRIVATE_KEY**  
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

要查看当前工作空间下所有的文章，只需执行：

```
ignotion -l
```

或

```
ignotion --list
```

该指令默认按时间顺序列出所有文章，若要以文件名顺序列出文章，请执行：

```
ignotion -l --name-order
```


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

在Front Matter中，你可以指定这篇文章的标题，使之区别于文件名。  
也可以指定渲染这篇文章所使用的模版。


## 转译

```
absss
```

## 远程目录与上载

正文正文正文正文正文正文正文正文正文  
正文正文正文正文正文正文正文正文正文 
