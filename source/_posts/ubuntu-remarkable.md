---
title:          Ubuntu下Markdown编辑器的安装
date:         2015-09-28 08:02:19
author:     孙宏伟
summary:    markdown Ubuntu 
categories: Remarkable
thumbnail:  Ubuntu
tags:
 - Ubuntu
 - markdown
 - remarkable
---


## 下载

&ensp; &ensp; 前往[remarkable](https://remarkableapp.github.io/linux/download.html)下载安装文件或([点此下载](https://remarkableapp.github.io/files/remarkable_1.87_all.deb))，Ubuntu系统选择*.deb格式:

 
 ![DownLoad Remarkable](download.png)

--- 
 
## 安装

&ensp; &ensp; 下载完成后，打开终端找到文件所在目录，执行如下命令进行安装，终端会输出一些报错信息，是由于安装缺少依赖导致的:


``` bash
$ sudo dpkg -i remarkable_1.87_all.deb
```

 ![Install Remarkable](install.png)

--- 

## 更新源

{% asset_img aaa.jpg markdown %}

&ensp; &ensp; 安装依赖前先更新一下源:

``` bash
$ sudo apt-get update
```

 ![Update Source](update.png)

--- 
 

## 安装依赖

&ensp; &ensp; 补充安装依赖项：
``` bash
$  sudo apt-get install -f
```
 
 ![Update Source](depend.png)

--- 
 
## 运行

&ensp; &ensp;在终端启动，即可使用Remarkable：
``` bash
$  remarkable
```
 
 ![Update Source](remarkable.png)

--- 
 
