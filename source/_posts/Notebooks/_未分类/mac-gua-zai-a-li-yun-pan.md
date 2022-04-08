---
link: http://hekun97@github.io/2021/12/27/mac-gua-zai-a-li-yun-pan/index.html
title: Mac阿里云盘挂载本地
description: 前言使用webdav协议将阿里云盘挂载本地，可以让阿里云盘变身为webdav协议的文件服务器。基于此，可以把阿里云盘挂载为Windows、Linux、Mac系统的磁盘，可以通过NAS系统做文件管理或文件同步和更多玩法，本篇主要是针对Mac系统的教程。  准备工作 Java环境 本次使用Jar包运行，因此需要Java环境，如何部署Java环境此处不进行赘述，网上很多教程，打开终端使用java -ve
keywords: WebDAV
author: 专业治头秃
date: 2021-12-27T06:27:32.000Z
publisher: 专业治头秃的博客
stats: paragraph=44 sentences=44, words=121
---
# 前言

使用webdav协议将阿里云盘挂载本地，可以让阿里云盘变身为webdav协议的文件服务器。基于此，可以把阿里云盘挂载为Windows、Linux、Mac系统的磁盘，可以通过NAS系统做文件管理或文件同步和更多玩法，本篇主要是针对Mac系统的教程。

![](https://cdn.jsdelivr.net/gh/hekun97/picture/Mac_aly_note/image-20211227143540198.png)

# 准备工作

1. Java环境 本次使用Jar包运行，因此需要Java环境，如何部署Java环境此处不进行赘述，网上很多教程，打开终端使用 `java -version`命令确认是否有Java环境。 ![](https://cdn.jsdelivr.net/gh/hekun97/picture/Mac_aly_note/image-20211227144357075.png)
2. `webdav-aliyundriver` 感谢zxbu大佬开源的项目，[点击下载项目](https://github.com/zxbu/webdav-aliyundriver/releases/latest)，并阅读其中的 `readme.md`对该项目进行熟悉。 ![](https://cdn.jsdelivr.net/gh/hekun97/picture/Mac_aly_note/image-20211227144905005.png)
> 建议自己下载源码编译，以获得最新代码，如果是下载的源码，建议打开后，[对本地文件夹进行修改](#更改本地文件夹)。
3. CloudMounter 可使用WebDAV协议挂载阿里网盘，选择他主要是觉得比较好用，也可以选择其它的，[下载链接](https://www.macwk.com/soft/cloudmounter)。![](https://cdn.jsdelivr.net/gh/hekun97/picture/Mac_aly_note/image-20211227152459255.png)

# 开始配置

## 获取refreshToken

1. 先通过浏览器（建议chrome）打开阿里云盘官网并登录：[https://www.aliyundrive.com/drive/](https://www.aliyundrive.com/drive/)
2. 登录成功后，按F12打开开发者工具，点击Application，点击Local Storage，点击 Local Storage下的 `https://www.aliyundrive.com/`，点击右边的token，此时可以看到里面的数据，其中就有refresh_token，把其值复制出来即可。（格式为小写字母和数字，不要复制双引号。例子：ca6bf2175d73as2188efg81f87e55f11）
3. 第二步有点繁琐，大家结合下面的截图就看懂了
![](https://cdn.jsdelivr.net/gh/hekun97/picture/Mac_aly_note/119246278-e6760880-bbb2-11eb-877c-aca16cf75d89.png)

> 该步参考[项目地址](https://github.com/zxbu/webdav-aliyundrive) `readme.md`中的内容。

## 运行

1. 找到下载或打包好的jar包，打开终端，进入jar包位置的路径，然后使用下面的命令运行项目。

```
这里的webdav.jar就是下载或打包好的jar包名称，不一致修改为一致即可
sudo java -jar webdav.jar --aliyundrive.refresh-token="your refreshToken"
```

![](https://cdn.jsdelivr.net/gh/hekun97/picture/Mac_aly_note/image-20211227151921835.png)

1. 打开浏览器查看是否正常 ![](https://cdn.jsdelivr.net/gh/hekun97/picture/Mac_aly_note/image-20211227152154666.png)

> 第一次打开会要求输入用户名和密码，默认都是admin。
![](https://cdn.jsdelivr.net/gh/hekun97/picture/Mac_aly_note/image-20211227165530623.png)

## 用CloudMounter连接

打开CloudMounter，选择WebDAV，然后连接到阿里云盘，再打开访达页面就和我最开始的一样了。
![](https://cdn.jsdelivr.net/gh/hekun97/picture/Mac_aly_note/image-20211227152632386.png)
> 注意运行项目的终端窗口一直不要关闭，另外图中的用户密码默认也都是admin。

# 优化

## 开机自启动

要一直保持运行项目的终端窗口不能关闭，且不能开机自启动显然不够优雅，所以可以使用脚本命令设置为开机自启动。

1. 建立脚本文件： `webdav.sh`；

```
# 进入到jar包所在文件夹位置
cd /Users/hk/Documents/webdav  
#"nohup XXX &"可以让你的命令在后台持续运行，终端关闭也没问题
nohup java -jar webdav.jar --aliyundrive.refresh-token="dca09cb094cd487ba5f88ef5b5848fb3" &
```
2. 设置开机自启动。 首先打开"系统偏好设置–>用户与群组–>登录项"，然后点击 `+`，把 `webdav.sh`文件加入到登录项即可。![](https://cdn.jsdelivr.net/gh/hekun97/picture/Mac_aly_note/image-20211227153748641.png)

## 关闭挂载服务

我们设置了开机自启动，当对源码进行更改后，需要停止服务，重新打包运行，那么就要先把项目进程关闭，可按以下操作。

### 方法一

1. 打开终端，查找使用8080端口的进程名有哪些。

```
查找使用8080端口的进程lsof -i tcP:8080
```
2. 找到其中java进程的pid，然后杀掉

```
杀掉 583 进程kill 583
```

![](https://cdn.jsdelivr.net/gh/hekun97/picture/Mac_aly_note/image-20211227154259947.png)

> 对于shell语句不熟悉的，可以把查找进程这条命令也加入到 `webdav.sh`中，然后在该脚本同目录下的 `nohup.out`文件中会进行记录，这样需要停止服务的时候进去看下是那个进程就可以了。

### 方法二

还有个更简单的方法，打开活动监视器，然后搜索java就可以找到对应的进程并结束，我用上面的方法最主要的原因是一开始不知道该项目运行后的进程叫啥。
![](https://cdn.jsdelivr.net/gh/hekun97/picture/Mac_aly_note/image-20211227204433101.png)

## 更改本地文件夹

改一下这个本地文件夹，默认是在 `/etc/`下，在Mac系统中可能会有权限问题。

1. 更改源码

![](https://cdn.jsdelivr.net/gh/hekun97/picture/Mac_aly_note/image-20211227145914311.png)

1. 打包![](https://cdn.jsdelivr.net/gh/hekun97/picture/Mac_aly_note/image-20211227150052118.png)

> 推荐有Java项目开发经验的搞。

## 更改端口号

一直在后台开启会占用8080默认端口号，我们在开发别的项目时，就很不方便，所以最好把端口号进行修改。

### 方法一

通过在 `application.properties`配置文件中添加一行 `server.port=8000`，修改成我们想要的端口号即可。
![](https://cdn.jsdelivr.net/gh/hekun97/picture/Mac_aly_note/image-20211227170106038.png)
> 同时在这里也可以对登录的用户名和密码进行修改。

### 方法二

更简单的方法，直接在启动项目时，将 `server.port`拼在后面

```
java -jar webdav.jar --aliyundrive.refresh-token="dca09cb094cd487ba5f88ef5b5848fb3" --server.port=8010
```

![](https://cdn.jsdelivr.net/gh/hekun97/picture/Mac_aly_note/image-20211227202957434.png)

## 自动化

### 退出终端

虽然我们已经优化为[开机自启动](#开机自启动)了，但是开机后的终端运行 `webdav.sh`脚本后，并不会关闭终端窗口并退出软件。因此这里我使用了 `Keyboard Maestro`软件（以下简称KM）添加了自动化操作来关闭终端。
![](https://cdn.jsdelivr.net/gh/hekun97/picture/Mac_aly_note/image-20220113130656853.png)

### 挂载云盘

在实际使用过程中，我发现如果只是把CloudMounter设置为开机自启动，虽然在软件中设置了启动时自动挂载云盘，但实际上，因为 `webdav.sh`脚本需要一定时间才能执行成功，所以会导致CloudMounter不能完成启动自动挂载云盘。
![](https://cdn.jsdelivr.net/gh/hekun97/picture/Mac_aly_note/image-20220113132306824.png)

这里也是使用了KM软件来完成等待一段时间后，再启动CloudMounter，此时 `webdav.sh`脚本也已经运行成功，所以实现了启动就挂载好云盘，不用我们再去手动挂载了。
![](https://cdn.jsdelivr.net/gh/hekun97/picture/Mac_aly_note/image-20220113131437548.png)
