---
title:      Ubuntu下remarkable的安装
date:       2018-10-09 12:02:19
author:     孙宏伟
summary:    markdown Ubuntu 
categories: Ubuntu
thumbnail:  Ubuntu
tags:
 - Ubuntu
 - markdown
 - remarkable
---


## 下载

&ensp; &ensp; 前往[remarkable](https://remarkableapp.github.io/linux/download.html)下载安装文件或([点此下载](https://remarkableapp.github.io/files/remarkable_1.87_all.deb))，Ubuntu系统选择*.deb格式:

 
 ![DownLoad Remarkable](/home/sun/blog/source/_posts/ubuntu-markdowndownload.png)

--- 
 
## 安装

&ensp; &ensp; 下载完成后，打开终端找到文件所在目录，执行如下命令进行安装，终端会输出一些报错信息，是由于安装缺少依赖导致的:


``` bash
$ sudo dpkg -i remarkable_1.87_all.deb
```
 
 ![Install Remarkable](https://github.com/sunhw41/sunhw41.github.io/blob/master/img/2018-09-10_02.png?raw=true)

--- 

## 更新源

&ensp; &ensp; 安装依赖前先更新一下源:

``` bash
$ sudo apt-get update
```

 ![Update Source](https://github.com/sunhw41/sunhw41.github.io/blob/master/img/2018-09-10_03.png?raw=true)

--- 
 

## 安装依赖

&ensp; &ensp; 补充安装依赖项：
``` bash
$  sudo apt-get install -f
```
 
 ![Update Source](https://github.com/sunhw41/sunhw41.github.io/blob/master/img/2018-09-10_04.png?raw=true)

--- 
 
## 运行

&ensp; &ensp;在终端启动，即可使用Remarkable：
``` bash
$  remarkable
```
 
 ![Update Source](https://github.com/sunhw41/sunhw41.github.io/blob/master/img/2018-09-10_05.png?raw=true)

--- 
 
