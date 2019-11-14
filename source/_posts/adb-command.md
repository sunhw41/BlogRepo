---
title:      ADB常用调试命令
date:       2019-10-21 15:31:19
author:     孙宏伟
summary:    ADB debug
categories: Android
tags:
 - ADB
---

&ensp;&ensp;&ensp;&ensp;首先看下官方的介绍:

>&ensp;&ensp;Android Debug Bridge (adb) is a versatile command line tool that lets you communicate with an emulator instance or connected Android-powered device. It is a client-server program that includes three components:
&ensp;&ensp; A client, which runs on your development machine. You can invoke a client from a shell by issuing an adb command. Other Android tools such as the ADT plugin and DDMS also create adb clients.
&ensp;&ensp;A server, which runs as a background process on your development machine. The server manages communication between the client and the adb daemon running on an emulator or device.
&ensp;&ensp;A daemon, which runs as a background process on each emulator or device instance.

>&ensp;&ensp; You can find the adb tool in <sdk>/platform-tools/.

&ensp;&ensp;&ensp;&ensp;大致就是说ADB是个多功能的命令行工具,可以连接到模拟器或者Android设备,由以下三个模块组成:
&ensp;&ensp;&ensp;&ensp;一个运行在开发机器上的Client,可以通过在shell中输入ADB命令启动一个ADB客户端,ADT插件或者DDMS同样可以启动一个ADB的客户端;
&ensp;&ensp;&ensp;&ensp;一个运行在开发机器上的Server,以后台的方式运行,用来管理Client和运行在模拟器或者Android设备上的Daemon之间的通信;
&ensp;&ensp;&ensp;&ensp;一个运行在模拟器或者真实Android设备上的后台程序.
&ensp;&ensp;&ensp;&ensp;ADB工具一般位于<em style="color:red">  \{sdk\}/platform-tools/.</em>
## Android设备连接相关指令

### 无线调试连接
```bash
$adb  connect ip:port
```

### 与设备断开连接
```bash
$adb  disconnect
```

### 终止adb进程
```bash
$adb  kill-server
```

## Android应用调试相关指令
### 安装应用
```bash
$adb  install -t -r ***.apk 
```

### 删除应用
```bash
$adb  shell pm uninstall PackangeName 
```
PackangeName为要删除的应用的具体包名;
### 查看包名
```bash
$adb  shell pm list packages
```
 如需删除应用时,不知道具体应用的包名,可以通过该命令将系统内所有应用的包名列出来;
### 拉起应用
```bash
$adb shell am start PackageName/.ActivityName
```
例如当前应用的包名为"com.sun.myapplication",要拉起的Acitivity,在当前包的目录下,且名称为"MainActivity",则命令如下:
```bash
$adb shell am start com.sun.myapplication/.MainActivity
```
### 拉起Service
```bash
$adb -s shell am startservice -a START_XXX_SERVICE
```

### 发送广播
```bash
$adb shell am broadcast -a RECEIVE_BROADCAST
```

### 查看当前多少个设备连接
```bash
$adb devices
```

### 对指定设备进行操作
```bash
$adb -s adnroiddevicename XXX XXX
```
通常我们只连接一个Android设备的话无需此步骤,上述命令均可正常使用. 但是当同时连接多个Android设备时,再直接用上述命令则会发生错误,提示存在不只一个Android设备,需要指定具体哪一个,那就需要在上述命令的基础上,执行此命令,列出所有设备,然后再增加一个 -s 的参数没来指定具体对哪个设备进行操作,例如,一个通过wifi进行adb连接的设备为"10.10.10.123:5555",则安装应用的命令如下:
```bash
$adb -s 10.10.123.123 install -t -r ***.apk
```

## Android文件操作
### 获取Root权限
```bash
$adb root
$adb remount
```
执行上述命令后,即可在外部重新挂在Android设备,可以通过相关命令对Android系统进行文件的拉取和推送;

### 拉取文件
```bash
$adb pull /***/***/*** .
```
该命令将系统内某文件夹下的文件拉取到电脑中,例如需要将Android系统内/etc/resolve.conf文件拉取出来进行编辑,则命令如下:
```bash
$adb pull /etc/resolve.conf  .
```
同理用上述方法也可以将Android系统内的应用拉取出来.

### 推送文件
```bash
$adb push *** /***/***/***
```
该命令适用于将电脑内的某文件推送到安卓系统中,例如将某个音乐文件推送到系统内的某个文件夹,则命令如下:
```bash
$adb push moonlight.mp3 storage/emulated/0/kwmusiccar/
```
## Android shell
### 命令行交互
```bash
$adb shell
```
通过上述命令,可以进入到命令行交互的界面,直接对Android 系统的内容进行查看;
### shell内编辑文件
```bash
$mount -o remount,rw /
```
当进入到shell界面时,由于文件系统的限制,还不能直接对系统内的文件进行编辑,执行上述指令后,即可直接在shell内对文件进行编辑操作;

## 查看Log
### 打印全部Log
```bash
$adb shell logcat
```

### 选择性打印Log
```bash
$adb shell logcat |　grep sunhw
```
上述命令可以过滤Log中所有包含＂sunhw＂字段的内容；当需要再进一步精确，例如只打印所有通过Log.d打印出来的包含＂sunhw＂字段的Log,执行下述命令即可：
```bash
$adb shell logcat *:D |　grep sunhw
```