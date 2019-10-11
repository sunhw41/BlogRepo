---
title:      NVMe硬盘上安装Ubuntu
date:       2019-10-08 19:17:20
author:     孙宏伟
summary:    Install Ubuntu On NVMe
categories:  Ubuntu
tags:
 - Ubuntu
---


## 在NVMe硬盘上安装Ubuntu

### 现象
&ensp;&ensp;&ensp;&ensp;今天在帮同事安装Ubuntu时遇到点困难,整理一下.同事的电脑是Dell inspire 5488,18年生产的.因为开发工具原因我们需要使用Ubuntu16.04(Kernel:4.15.0-29).因为是同事电脑,安装时没拍照,安装好后也不好再折腾一遍,就纯文字描述了.

&ensp;&ensp;&ensp;&ensp;一开始采用UEFI的方式安装,启动后进入BIOS,发现了两个安装的U盘,随意选一个进入下一步,结果往下进行后提示如下:
>安装Ubuntu需要8.3G的控空间,而磁盘只有4G

&ensp;&ensp;&ensp;&ensp;以为是启动时的U盘选差了, 重启再选另外一个,仍然是这个原因,重新给U盘烧写系统仍是上述现象.

&ensp;&ensp;&ensp;&ensp;后来决定放弃使用UEFI模式启动,使用Legacy方式,虽然可以安装系统,但是启动后提示找不到启动的设备.没法发现电脑的硬盘.

---

### 原因
&ensp;&ensp;&ensp;&ensp;发送上述现象是因为该电脑为固态硬盘,BIOS中硬盘模式开启了Rapid ON的模式,硬盘在Linux系统中不是传统的 /dev/sd* 这样的形式存在的,所以找不到硬盘.

---

### 解决方法
&ensp;&ensp;&ensp;&ensp;将BIOS的启动参数进行如下设置:

>1. 采用Legacy方式启动;
>1. 将硬盘模式更改为ACHI;
>1. 将UEFI Boot Security 更改为Off;

&ensp;&ensp;&ensp;&ensp;然后重启进入BIOS界面,会有Legacy启动选项和UEFI启动选项,选择UEFI选项下的U盘作为启动介质,此时会提示在非UEFI模式下选择采用UEFI模式安装,同意该方式,继续下一步,直至安装结束.

&ensp;&ensp;&ensp;&ensp;重启后进入到BIOS看一下,是否还存在Legacy这个启动选项,如果存在的话则将该方式关闭,并且将UEFI中的Security Boot 更改为Off即可正常使用.

---

### 关于UEFI和Leagacy
>UEFI技术较新,只支持64位操作系统,启动速度较快;

>Legacy是传统的启动模式,不能支持超过2T的硬盘;

&ensp;&ensp;&ensp;&ensp;更多区别和细节就百度一下吧,不细说了.
