---
link: https://blog.csdn.net/xujiuba/article/details/107182028
title: Mac 安装 Java jdk 环境配置
description: 目录1、验证2、下载获取Mac版本的Java安装包3、安装双击已经下载好的dmg文件进行安装双击.pkg文件安装完成4、环境配置Mac在安装jdk的时候自动配置好了验证是否成功5、Mac下查看已安装的jdk版本及其安装目录1、验证判断当前Mac是否安装了jdk如果出现以下情况表示还未安装jdk2、下载获取Mac版本的Java安装包推荐地址：https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-213315
keywords: jdkmac安装
author: Xujiuba Csdn认证博客专家 Csdn认证企业博客 码龄4年 企业员工
date: 2020-07-07T08:50:12.000Z
publisher: null
stats: paragraph=26 sentences=17, words=76
---
### 安装 Java jdk

* [1、验证](#1-1)
- [是否有 jdk](#-jdk-2)
* [2、下载](#2-6)
- [获取Mac版本的Java安装包](#macjava-7)
* [3、安装](#3-12)
  - [双击已经下载好的dmg文件进行安装](#dmg-13)
  - [双击.pkg文件](#pkg-15)
  - [安装完成](#-17)
* [4、环境配置](#4-19)
  - [Mac在安装jdk的时候自动配置好了](#macjdk-22)
  - [验证是否成功](#-24)
* [5、Mac下查看已安装的jdk版本及其安装目录](#5macjdk-30)

# 1、验证

## 是否有 jdk

判断当前Mac是否安装了jdk
如果出现以下情况表示还未安装jdk
![](https://img-blog.csdnimg.cn/20200707152333604.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1aml1YmE=,size_16,color_FFFFFF,t_70)

# <a name="2_6">;</a>  2、下载

## 获取Mac版本的Java安装包

推荐地址：[https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
这边是8u251版本，下载的时候可能需要注册一个Oracle账户登录后，才可以进行下载
![](https://img-blog.csdnimg.cn/20200707151549467.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1aml1YmE=,size_16,color_FFFFFF,t_70)
备注：下载的时间比较久，在mac上的下载会比较慢

# <a name="3_12">;</a>  3、安装

## 双击已经下载好的dmg文件进行安装

![](https://img-blog.csdnimg.cn/2020070715223888.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1aml1YmE=,size_16,color_FFFFFF,t_70)

## <a name="pkg_15">;</a> 双击.pkg文件

![](https://img-blog.csdnimg.cn/20200707152720204.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1aml1YmE=,size_16,color_FFFFFF,t_70)

## 安装完成

![](https://img-blog.csdnimg.cn/20200707152609916.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1aml1YmE=,size_16,color_FFFFFF,t_70)

# <a name="4_19">;</a>  4、环境配置

1、MAC的环境变量的配置都是在终端理进行，按键盘"Ctrl + 空格"组合键，调出Spotlight搜索，在这里可以快速启动终端，输入 `ter&#xFF08;terminal.app&#xFF09;`,然后回车，即可打开终端：
![](https://img-blog.csdnimg.cn/2020070716222455.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1aml1YmE=,size_16,color_FFFFFF,t_70)

## Mac在安装jdk的时候自动配置好了

所以省略了配置环境的步骤

## 验证是否成功

在终端输入 `java`，验证是否成功安装了java。显示以下信息表示正确
![](https://img-blog.csdnimg.cn/20200707163710353.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1aml1YmE=,size_16,color_FFFFFF,t_70)
接下来输入 `javac`验证是否成功配置好环境变量。显示以下信息表示正确。
![](https://img-blog.csdnimg.cn/20200707163842538.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1aml1YmE=,size_16,color_FFFFFF,t_70)
如果没有配置成功，可以手动找到JDK的本地安装目录，然后进行配置

# <a name="5macjdk_30">;</a>  5、Mac下查看已安装的jdk版本及其安装目录

可以通过在命令行输入 `java -version`查看是否安装了jdk

按键盘"Ctrl + 空格"组合键，调出Spotlight搜索输入 `ter&#xFF08;terminal.app&#xFF09;`，打开终端输入： `/usr/libexec/java_home -V`

注意：输入命令参数区分大小写(-v是不对的，必须是-V)

如图：3个红框内依次为：输入命令； 当前Mac已安装jdk目录； Mac默认使用的jdk版本；
![](https://img-blog.csdnimg.cn/20200707163423642.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1aml1YmE=,size_16,color_FFFFFF,t_70)
