---
title:        OSX下解决Gradle同步失败的问题
date:       2018-08-03 08:04:56
author:     孙宏伟
categories: Android
tags:
 - OSX
 - Android Studio
---


## 1、下载Android Studio
&ensp; &ensp;&ensp; &ensp;  OSX下Android Studio的安装过程就不多叙述了,和安装其他软件方法一样,需要注意的是国外的Android开发者网站被封了,这里提供一个Android Studio的[下载地址](https://developer.android.google.cn/studio/).

![DownLoad Android Studio](download.png)

## 2、安装Android Studio
&ensp; &ensp;&ensp; &ensp; 我下载的是“android-studio-ide-173.4819257-mac.dmg”,下载好安装文件后双击,然后将其拖到App文件夹即可使用.

![install Android Studio](install.png)

## 3、下载复制Gradle文件

&ensp; &ensp; &ensp; &ensp; 但是在第一次启动Android Studio构建项目常常会出现卡住下载不动或者失败的的情况,下面介绍下如何解决这个问题.

&ensp; &ensp;&ensp; &ensp; 首先需要找到“.gradle”目录,大部分位于“~/”目录下,进入"/Users/<em style="color: red">sun</em>/.gradle/wrapper/dists/gradle-4.4-all/<em style="color:red">9br9xq1tocpiv8o6njlyu5op1</em>",其中<em style="color:red">红色字体</em>部分是我自己电脑的情况,可能会有不同,osx下使用"**shift+command+.**"可以查看隐藏的文件夹,进入到该文件夹删除文件夹内<em style="color:#FF00FF
">".part"</em>文件:

![delete .part file](gradlepath.png)

&ensp; &ensp;&ensp; &ensp; 然后登陆到[gradle资源](https://services.gradle.org/distributions)的网站下载对应的[gradle-4.4-all.zip](https://services.gradle.org/distributions/gradle-4.4-all.zip),下载后不需要解压,直接复制到上述文件夹中.

![gradle download](gradlefile.png)


## 4、重新启动Android Studio

&ensp; &ensp; &ensp; &ensp; 重新启动Android Studio即可解决gradle构建失败或者卡住的问题了.

![run Android Studio](androidstudio.png)
