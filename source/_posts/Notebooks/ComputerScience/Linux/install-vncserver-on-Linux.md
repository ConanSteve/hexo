---
title: Ubuntu 20.04 安装vncserver
date: 2022-06-20 10:00:00
author: 陌上人如玉
comments:
description:
keywords:
top_img:
cover:
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
tags: 
categories: Linux
---


# 安装

```shell
su root
apt update
sudo apt install xfce4 xfce4-goodies
sudo apt install tightvncserver
```
# 启动
```shell
vncserver :5
```

# 关闭
```shell
vncserver -kill :5
```
# 自定义分辨率
## 1080P
将以下配置保存为`.vnc.sh`，然后运行`sh .vnc.sh`即可
```shell
#!bin/bash
vncserver -geometry 1920x1080 -depth 24
```
或者
```shell
vncserver -geometry 1920x1080 -depth 24 :5
```

## 4K
将以下配置保存为`.vnc4.sh`，然后运行`sh .vnc4.sh`即可
```shell
#!/bin/bash
vncserver -geometry 3840x2160 -depth 24
```
# 下载
## VNC Viewer
官网只有最新下载地址，如果需要下载历史版本，更改下面的链接为对应版本即可。如`6.21.406`为MacOS 10.13.6最大支持版本。
`https://downloads.realvnc.com/download/file/viewer.files/VNC-Viewer-6.21.406-MacOSX-x86_64.dmg`
## VNC Server
同理可下载历史版本
`https://downloads.realvnc.com/download/file/vnc.files/VNC-Server-6.9.1-MacOSX-x86_64.pkg`

# Reference

1. [vnc server配置、启动、重启与连接](https://www.cnblogs.com/wangyuehan/p/9807628.html)
2. [18安装教程](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-vnc-on-ubuntu-18-04)
3. [常用命令](https://blog.csdn.net/techsupporter/article/details/52887199)
4. [白屏](https://jingyan.baidu.com/article/cbcede077f59bf02f40b4ddb.html)
5. [Win10子系统-Ubuntu安装及配置VNC访问XFCE4桌面](https://blog.csdn.net/qq_24253277/article/details/103943848)
6. [给Ubuntu服务器版安装GNOME桌面](https://www.linuxidc.com/linux/2018-01/150471.htm)
7. [在服务器上安装图形化桌面](https://blog.csdn.net/m0_37622530/article/details/102632151)