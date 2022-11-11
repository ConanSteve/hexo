---
title: Linux
date: 2022-02-01 10:00:00
author: ConanSteve
categories: Linux
---

# unix系统发展分支图

![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011530839.png)

# shell 命令

 [linux命令大全](https://www.runoob.com/linux/linux-command-manual.html)

 [windows商店安装ubuntu教程](https://blog.csdn.net/sun___shy/article/details/80917092)

 [wsl安装](https://blog.csdn.net/saisai_in_csdn/article/details/106610039)

[shell 脚本编程](https://www.cnblogs.com/zhang-jun-jie/p/9266858.html)



## [wget命令详解](https://www.cnblogs.com/sx66/p/11887022.html)

```Bash
# -O 保存文件名
wget -O $fileName '$url'
```

查看系统信息：` neofetch`

## [查看文件夹大小](https://blog.csdn.net/qq_27003337/article/details/108282745)

[shell 查看文件夹/文件大小、目录/文件数量](https://blog.csdn.net/qq_27003337/article/details/108282745)

```Bash
# du -sh $folderpath 
du -sh ./.git
```

# 必装软件

[windows10 WSL初体验（含vim、makefile）_qq_43126480的博客-CSDN博客](https://blog.csdn.net/qq_43126480/article/details/102957219)

```Bash
sudo apt install neofetch
sudo apt install zsh
sudo apt-get install openssh-server  ip
sudo apt-get install g++
```

[sshserver](https://cloud.tencent.com/developer/article/1751149#:~:text=Ubuntu缺省没有安装SSH Server，使用以下命令安装： sudo apt-get,install openssh-server 然后确认sshserver是否启动了：（或用“netstat -tlp”命令）)

更换git源

```Groovy
sudo cp /etc/apt/sources.list /etc/apt/sources.list.20211128
sudo vim /etc/apt/sources.list
:set nu
gg
dG
```

[Ubuntu 更换 apt 源为阿里云_sigmarising的博客-CSDN博客_ubuntu换源阿里云](https://blog.csdn.net/sigmarising/article/details/84778296)

## 开机启动

[ubuntu start](https://www.cnblogs.com/dhcn/p/11523914.html)

## 用户管理

[用户管理](https://blog.csdn.net/qq_31456593/article/details/79247366)

修改用户密码 `passwd username `



### idea

[远程调试](https://www.jianshu.com/p/302dc10217c0)






# Others

## 深度学习相关

Linux 查看显卡信息

 `lspci | grep -i vga`

 `lspci | grep -i nvidia`

 查看 GPU 使用情况

 静态查看 `nvidia-smi`

 周期性查看 `watch -n 10 nvidia-smi `命令行参数-n 后边跟的是执行命令的周期，以 s 为单位

[在Linux服务器上跑机器学习代码相关操作](https://www.jianshu.com/p/deb91cc253ea)

## 后台运行程序

[后台跑代码](https://blog.csdn.net/weixin_43269020/article/details/83819687)

python test.py > test.log 2>&1 &

nohup python src.py >src.log 2>&1 &

**实现屏幕输出记录到日志文件**

```
nohup yourcommand 2>&1 &
```

\# 0 – stdin (standard input)，1 – stdout (standard output)，2 – stderr (standard error) ；

\# 2>&1是将标准错误（2）重定向到标准输出（&1），标准输出（&1）再被重定向输入到[日志](https://so.csdn.net/so/search?q=日志&spm=1001.2101.3001.7020)文件中。

如果希望将日志输出到别的文件中，可以增加一个文件路径参数。如下：

```
nohup yourcommand > myout.log 2>&1 &
```

其中myout.log是保存输出的文件名称；

[参考](https://blog.csdn.net/cxu123321/article/details/108727075)

**实时监测日志输出内容命令：tail**

## 发行版

### ubuntu

[截图](https://www.jb51.net/os/Ubuntu/421276.html)

 [修改苹果字体](https://blog.csdn.net/qq183837971/article/details/78235144)

 [安装苹果主题](https://www.linuxmi.com/ubuntu-20-04-mac-os-catalina.html)

 [系统美化1](https://zhuanlan.zhihu.com/p/35362159)

 [系统美化2](https://zhuanlan.zhihu.com/p/68921091)

 [ubuntu 安装 火狐浏览器（中国版本）](https://www.cnblogs.com/spqin/p/13061508.html)

 [/mnt/hgfs/下不显示共享文件夹的处理办法](https://blog.csdn.net/qq_33733970/article/details/84326110?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param)

[Ubuntu 16.04 禁用 nouveau 安装 nvidia显卡驱动](https://blog.csdn.net/u012442845/article/details/78855573)

> 要先安装 gcc，make 包

> [reference1](https://www.cnblogs.com/xuyaowen/p/linux-secure-boot-disable.html)

>  （ https://blog.csdn.net/wangyjfrecky/article/details/84029668?utm_medium=distribute.pc_relevant.none-task-blog-title-4&spm=1001.2101.3001.4242）

> [挂载磁盘](https://blog.csdn.net/tsq292978891/article/details/84503718) 

### idea 安装

[idea安装](https://www.cnblogs.com/doggod/p/11892899.html)

 [Ubuntu18.04 安装 Idea 2018.2 Ultimate](https://blog.csdn.net/weixx3/article/details/81136822)

 [ubuntu中PyCharm的安装与卸载](https://blog.csdn.net/weixin_31484477/article/details/81133590)

### deepwine

[ubuntu20.04安装微信](https://www.cnblogs.com/mrwuzs/p/13200462.html)

 [Deepin-wine的相关操作](https://www.deep-os.com/?id=18)

 [调整微信分辨率](https://blog.csdn.net/w851685279/article/details/105892373/)

### java

[install](https://www.cnblogs.com/powerwu/articles/12028350.html)

 [Maven](https://www.cnblogs.com/kxm87/p/9686097.html)

# WSL

[重置管理员密码](https://blog.csdn.net/qq_18625805/article/details/104779056)

#### 问题

 

 

 