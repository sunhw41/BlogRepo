---
title:        Ubuntu内核的安装、删除与切换
date:       2017-08-03 08:04:56
author:     孙宏伟
categories: Linux
tags:
 - Linux
 - Kernel
---

## 查看当前内核
&ensp; &ensp;&ensp; &ensp; 可以通过以下命令查看当前安装了几个linux内核：
```bash
$dpkg --get-selections | grep linux-image
```
![grepKernel](grepKernel.png) 

&ensp; &ensp;&ensp; &ensp; 当有多个内核时，使用如下命令查看当前使用的是哪个版本：
```bash
$uname -a
```
![uname](uname.png) 

## 配置启动顺序
&ensp; &ensp;&ensp; &ensp; 如果当前使用的内核为自己所需要的，无需做任何改动，如果电脑中有需要的内核，但是当前使用的不是，可以使用如下命令进行修改，首先查询需求内核的顺序：
```bash
$grep menuentry /boot/grub/grub.cfg 
```
![menuentry](menuentry.png) 
&ensp; &ensp;&ensp; &ensp; 在输出的结果中找到这样的行：

<em style="color:orange">menuentry 'Ubuntu, with Linux 4.8.0-36-generic' --class ubuntu.........</em>


&ensp; &ensp;&ensp; &ensp; 从0开始计算，找到自己所需要内核的顺序，假设在第4行，则序列为3(从0开始)，然后修改这个文件：
```bash
$sudo vim /etc/default/grub 
```
&ensp; &ensp;&ensp; &ensp; 找到<em style="color:red">“GRUB_DEFAULT=0”</em>这行，修改为<em style="color:red">“GRUB_DEFAULT=“1>3”</em>
或 <em style="color:red"> “GRUB_DEFAULT=”Ubuntu, with Linux 4.8.0-36-generic”(不推荐)</em>，然后保存：


&ensp; &ensp;&ensp; &ensp; 执行如下命令更新grub，然后重启，用uname查看当前的内核版本是否已经变更：
```bash
$sudo update-grub
```
&ensp; &ensp;&ensp; &ensp; 上述步骤对应的是系统启动是的GNU Grub的顺序，如果上述操作没生效，可以重启时按住Esc键，然后查看Ubuntu Advance的位置，进入后再查看所需要的内核的序号，然后更改按照下述方式更改：
<em style="color:red">GRUB_DEFAULT=“2>3”</em>
(从上向下数，从0开始，假设Ubuntu Advance位置为2,所需内核位置为3)

## 安装指定内核
&ensp; &ensp;&ensp; &ensp; 如果通过dpkg --get-selections 命令输出的内容没有所需要的内核，则需要新装，假设需要的内核版本为4.8.0-36，使用如下命令进行安装：
```bash
$sudo apt-get install linux-image-4.8.0-36-generic 
$sudo apt-get install linux-image-extra-4.8.0-36-generic
```
&ensp; &ensp;&ensp; &ensp; 内核成功安装后，再执行上述的命令讲自己的内核修改为默认启动即可

&ensp; &ensp;&ensp; &ensp; 当然也可以前往[LinuxKernel](https://mirrors.edge.kernel.org/pub/linux/kernel/) 下载合适的内核版本，本地编译安装，此处不做过多描述。

&ensp; &ensp;&ensp; &ensp; 如果由于安装时的设置，导致系统内核过多，占用/boot的空间，因此需要删除不必要的内核，执行以下命令删除即可    
```bash
$sudo apt-get purge linux-image-4.8.0-36-generic 
```
&ensp; &ensp;&ensp; &ensp; 使用remove也可以，但是不会删除配置文件，purge会删除相关的配置文件，避免留下冗余的内容，当尝试新内核时，由于新内核存在很多不稳定性，因此建议保留1～2个稳定的内核，以免意外。