---
title: Linux内核的编译方法
date: 2019-07-10 10:14:48
author:     孙宏伟
summary:    Linux compile guide
categories: Linux
tags:
 - Linux 
---

## Linux 版本号命名规则

&ensp;&ensp;&ensp;&ensp;这里先对linux的内核版本号做个解释，以“4.8.0-36-generic”为例：

<table>
   <tr>
      <td>4</td>
      <td>8</td>
      <td>0</td>
      <td>36</td>
      <td colspan="2">generic</td>   
   </tr>
   <tr>
      <td>主版本号</td>
      <td>奇数为开发版</td>
      <td>修订版本号</td>
      <td>第几次微调</td>
      <td>generic</td>
      <td>通用</td>
   </tr>
   <tr>
      <td></td>
      <td>偶数为稳定版</td>
      <td></td>
      <td></td>
      <td>preemption</td>
      <td>抢占式</td>
   </tr>
   <tr>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>preemption</td>
      <td>低延时</td>
   </tr>
   <tr>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>rt/realtime</td>
      <td>实时</td>
   </tr>
</table>

**对于该用哪种类型,官网上的解释如下:**

-  If you do not require low latency for your system then please use the -generic kernel.
-     If you need a low latency system (e.g. for recording audio) then please use the -preempt kernel as a fist choice. This reduces latency but doesn't sacrifice power saving features. It is available only for 64 bit systems (also called amd64).
-     If the -preempt kernel does not provide enough low latency for your needs (or you have an 32 bit system) then you should try the -lowlatency kernel.
-     If the -lowlatency kernel isn't enough then you should try the -rt kernel
-     If the -rt kernel isn't enough stable for you then you should try the -realtime kernel

## Linux 内核编译

&ensp;&ensp;&ensp;&ensp; 前往[Linux内核](https://mirrors.edge.kernel.org/pub/linux/kernel/) 选择所需要的版本:
![DownLoadLink](downlink.png)

&ensp;&ensp;&ensp;&ensp; 下载到本地执行下述命令解压,进入到解压后的文件夹:
``` bash
$tar -xvf linux-3.18.129.tar.xz linux-33.18.129
$cd linux-33.18.129
```

&ensp;&ensp;&ensp;&ensp;执行内核配置时需要依赖到curses的库，用于以图形化选择配置方案,执行如下命令安装:
```bash
$sudo apt-get install libncurses5-dev
```

&ensp;&ensp;&ensp;&ensp;对内核进行裁剪，执行如下命令进入到图形化配置界面，直接选择需要的项目进行更改，具体内容请查阅内核配置的详细文章,此处不做过多介绍:
```bash
$make menuconfig
```

&ensp;&ensp;&ensp;&ensp;根据自己的需求进行相应的配置，完成后会保存为.config到该目录，当然也可以拷贝已有的文件，不用再进行配置。
![MenuConfig](menuconfig.png)


&ensp;&ensp;&ensp;&ensp;执行编译命令，开始编译，如果是多cpu，可以后接 -j(n)，这样编译能快些，不然只会一个一个的编译:
```bash
$make -j4
```
&ensp;&ensp;&ensp;&ensp;编译完成后，执行如下命令安装内核modules:
```bash
$sudo make modules_install
```
&ensp;&ensp;&ensp;&ensp;执行完毕后可以到/lib/modules下查看是否新增了对应的文件夹:
![libmodule](libmodules.png)
&ensp;&ensp;&ensp;&ensp;然后再执行如下命令安装内核:
```bash
$sudo make install 
```
&ensp;&ensp;&ensp;&ensp;执行完毕后到/boot文件夹下查看是否新增相关文件:
![libmodule](boot.png)

## 使用新内核
&ensp;&ensp;&ensp;&ensp;安装完成后，重启机器。在重启的过程中，使用TAB+shift组合键或者ESC进入grub引导界面，不同的机器进入的方式可能会略有差异,以Ubuntu为例,启动时进入到grub,可以看到已经多出了本次编译的内核:
![grub](grub.png)
&ensp;&ensp;&ensp;&ensp;进入系统后再查看内核版本,已经变更为新编译的3.18.129:
![kernelversion](kernelversion.png)