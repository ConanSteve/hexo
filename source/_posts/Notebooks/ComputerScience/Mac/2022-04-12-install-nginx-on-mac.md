---
title: Mac安装并运行nginx
description: 
author: ConanSteve
date: 2022-04-12T08:28:06.000Z
---
## 1. 安装 brew

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

**【报错】：** Failed to connect to raw.githubusercontent.com port 443: Connection refused

**换个命令重新安装：**

```bash
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

（参考： _ [https://www.cnblogs.com/jiefangzhe/p/12929078.html](https://www.cnblogs.com/jiefangzhe/p/12929078.html)_）

**验证安装成功：**

```bash
brew -v
```

## 2. 安装 nginx

```bash
brew install nginx
```

**验证安装成功：**

```bash
nginx -v
```

## 3. 修改 nginx配置

**打开配置文件： `/usr/local/etc/nginx/nginx.conf`**
**1. 定义需要转发的服务地址：**

MacOS 12.1之后的配置存储位置为：`/opt/homebrew/etc/nginx/nginx.conf`

![](https://img-blog.csdnimg.cn/20201002161613502.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDYxNTE1NQ==,size_16,color_FFFFFF,t_70#pic_center)
**2. 配置请求转发：**![](https://img-blog.csdnimg.cn/20201002160855663.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDYxNTE1NQ==,size_16,color_FFFFFF,t_70#pic_center)

## 4. 运行 nginx


**1. 运行 nginx**

```bash
sudo nginx
```

**2. 重新加载 nginx**

```bash
sudo nginx -s reload
```

**3. 关闭 nginx**

```bash
sudo nginx -s stop
```



# Reference

1. https://blog.csdn.net/weixin_40615155/article/details/108901854
2. https://blog.csdn.net/weixin_45825077/article/details/107134300
2. [Nginx Linux详细安装部署教程](https://www.cnblogs.com/taiyonghai/p/6728707.html)



