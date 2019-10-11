---
title:  安装Ubuntu操作系统
date: 2019-10-10 19:56:23
author:     孙宏伟
summary:    install ubuntu system
categories: Ubuntu
tags:
 - Ubuntu
---

## 安装Ubuntu操作系统

&ensp;&ensp;&ensp;&ensp;一般可以直接将Ubuntu系统安装到磁盘上，或Ubuntu/Windows双系统，或在宿主机(当前电脑运行的系统)上安装虚拟机来运行Ubuntu，本文首先介绍一下虚拟机的安装,然后再讲解如何通过虚拟机引导Ubuntu镜像进行Ubuntu系统的安装,如果打算直接在电脑上安装Ubuntu,可以通过USB制成系统盘,然后[直接参考本部分](#jump)进行安装。对于双系统安装,只需在安装时选择选择保留Window,安装Ubuntu的选项即可,其他步骤完全相同,在此不再赘述.

### 一、安装虚拟机

&ensp;&ensp;&ensp;&ensp;1、前往VirtualBox网站下载安装包，根据宿主机的系统来下载安装程序，默认执行安装：
![DownLoadVirtualBox](downloadVirtual.png)

&ensp;&ensp;&ensp;&ensp;安装过程中会安装其他组件，用于网络和usb控制的，此类全部默认安装即可。



### 二、创建虚拟机
&ensp;&ensp;&ensp;&ensp;1、将Ubuntu镜像拷贝到本地，运行VirtualBox，点击“New”新创建一个虚拟机：
![CreateVirtualBox](CreateVirtualBox.png)

&ensp;&ensp;&ensp;&ensp;2、在弹出的对话框中输入新建虚拟机的名称，可自定义名称，选择虚拟机创建位置的文件夹，其他配置保持同图中一致，点击“Next”：
![NameSystem](NameSystem.png)

&ensp;&ensp;&ensp;&ensp;3、为本虚拟机分配内容，根据电脑实际情况分配，建议不要低于4G，点击“Next”：
![SetRam](SetRam.png)

&ensp;&ensp;&ensp;&ensp;4、为虚拟机分配虚拟硬盘文件，如图选择创建一个新的虚拟硬盘，点击“Next”：
![SetRom](SetRom.png)

&ensp;&ensp;&ensp;&ensp;5、选择新创建的虚拟硬盘类型，选择VDI，点击“Next”：
![SetRomType](SetRomType.png)

&ensp;&ensp;&ensp;&ensp;6、选择硬盘空间分配的模式，这里选择动态分配，硬盘文件的大小随着虚拟系统内文件的增多而增长，不会直接占用太多宿主机的空间，点击“Next”：
![SetStorage](SetStorage.png)

&ensp;&ensp;&ensp;&ensp;7、为虚拟硬盘命名，这里我们给硬盘分配100G的大小，该值是虚拟硬盘的最大容量，创建初期并不会一次性占用宿主机的100G空间，然后点击“Create”，完成虚拟机的创建：
![NameStorage](NameStorage.png)

### 三、配置虚拟机
&ensp;&ensp;&ensp;&ensp;1、创建完成后，在VirtualBox中选择刚刚创建的虚拟机，然后点击“Setting”：
![SettingSystem](SettingSystem.png)

&ensp;&ensp;&ensp;&ensp;2、在Setting界面，选择“Storatge”，然后点击“Controller：IDE”下方的光驱图标，再点击最右侧“Attributes”下“Optical Drive”后面的光驱图标，在弹出的对话框中选择”Choose Virtual Optical Disk File”，在新弹出的对话框中选择”ubuntu-16.04.2-desktop-amd64.iso”镜像文件，然后点击OK，至此完成虚拟机的启动镜像配置：
![SettingDetails](SettingDetails.png)

<span id="jump"> </span> 
### 四、安装Ubuntu系统

&ensp;&ensp;&ensp;&ensp;1、在VirtualBox中选择刚刚创建的虚拟系统，点击上方的“Start”，该虚拟系统启动：
![StartInstall](StartInstall.png)

&ensp;&ensp;&ensp;&ensp;2、等待系统加载启动镜像，加载过后如下图所示，可在左侧选择安装系统的语言，选择好系统的语言后，点击“Install Ubuntu”：

![InstallUbuntu](InstallUbuntu.png)

&ensp;&ensp;&ensp;&ensp;3、先不做任何配置，不要勾选任何选项，直接点击“continue”：
![ContinueInstall](ContinueInstall.png)

&ensp;&ensp;&ensp;&ensp;4、选择“Erase disk and install Ubuntu”，然后点击“Install Now”，在弹出的对话框中选择“Continue”：
![EraseInstall](EraseInstall.png)
![EraseContine](EraseContine.png)

&ensp;&ensp;&ensp;&ensp;5、选择时区，选择“Shanghai”为东8区，点击“Continue”：
![TimeZone](TimeZone.png)

&ensp;&ensp;&ensp;&ensp;6、选择键盘布局，默认点击“Continue”即可，该页面如果看不到“Continue”按钮，可以左右拖动键盘布局的对话框：
![KeyBoard](KeyBoard.png)

&ensp;&ensp;&ensp;&ensp;7、配置个人信息，然后点击“Continue”：
![PersonConfig](PersonConfig.png)

&ensp;&ensp;&ensp;&ensp;8、系统开始执行安装过程，此过程耗时较长，需要等待一段时间：
![Installing](Installing.png)

&ensp;&ensp;&ensp;&ensp;9、安装完成，点击“Restart Now”重启：

![InstallComplete](InstallComplete.png)

&ensp;&ensp;&ensp;&ensp;10、直接按Enter键即可重启：

![RestartSystem](RestartSystem.png)


&ensp;&ensp;&ensp;&ensp;11、重启后联网时会提示是否更新最新版本，注意点击不要更新：
![IgnoreUpdate](IgnoreUpdate.png)

### 五、安装拓展增强功能：

&ensp;&ensp;&ensp;&ensp;接下来为新安装虚拟系统安装拓展插件，用以实现跨系统的复制粘贴以及全屏等功能。
&ensp;&ensp;&ensp;&ensp;1、点击“Device”，选择“Insert Guest Additions CD image”，点击后会在虚拟系统中弹出如下的对话框点击“Run”进行安装：

![InstallAddition](InstallAddition.png)

&ensp;&ensp;&ensp;&ensp;2、点击“Run”后会弹出一个对话框，输入在安装时设置的密码，然后点击“Authenticate”开始进行安装：
![RunAddition](RunAddition.png)

&ensp;&ensp;&ensp;&ensp;3、安装过程中显示进度，当出现如下文字时，点击回车完成安装：
![AdditionComplete](AdditionComplete.png)

### 六、备注


&ensp;&ensp;&ensp;&ensp;因为不同的系统对应不同的内核,因此如果为了使用某些低版本的内核而安装了较早版本的操作系统,<em style="color:red">联网后会提示是否更新,此时不要进行更新</em>,因为更新会连带一起升级内核,会发送部分软件无法使用的现象.