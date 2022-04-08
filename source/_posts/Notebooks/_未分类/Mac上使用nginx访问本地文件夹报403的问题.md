---
link: https://blog.csdn.net/pxy20156/article/details/105516139
title: Mac上使用nginx访问本地文件夹报403的问题
description: 1. 安装并配置nginx1.1 安装nginxbrew install nginx安装成功后命令行提示可以使用brew services start nginx来启动nginx，也可直接使用nginx来启动。配置文件默认在/usr/local/etc/nginx/nginx.confnginx.conf的初始配置如下#user  nobody;worker_processe...
keywords: nginx访问文件夹403
author: Buptpxy Csdn认证博客专家 Csdn认证企业博客 码龄7年 暂无认证
date: 2020-04-14T10:22:34.000Z
publisher: null
stats: paragraph=76 sentences=82, words=321
---
# 1. 安装并配置nginx

## 1.1 安装nginx

`brew install nginx`
安装成功后命令行提示可以使用<br> `brew services start nginx`
来启动nginx，也可直接使用

```
nginx
```

来启动。配置文件默认在 `/usr/local/etc/nginx/nginx.conf`

nginx.conf的初始配置如下

```shell

worker_processes  1;

error_log  logs/error.log;
error_log  logs/error.log  notice;
error_log  logs/error.log  info;

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;

    sendfile        on;

    keepalive_timeout  65;

    server {
        listen       8080;
        server_name  localhost;

        location / {
            root   html;
            index  index.html index.htm;
        }

        location = /50x.html {
            root   html;
        }

    }

    include servers/*;
}
```

可以发现，此nginx默认监听8080端口（有的nginx监听的是80端口，视配置文件而定），当收到localhost:8080端口请求时，将其转发到html/index.html或html/index.htm，于是我们就看到了nginx的欢迎页面。

> 然而/usr/local/etc/nginx目录下并无html文件夹，说明这个相对目录相对的并不是/usr/local/etc/nginx目录，而是/usr/local/Cellar/nginx/1.17.9这个目录，这个目录下是有html文件夹的。
**`&#x6240;&#x4EE5;&#x5728;&#x914D;&#x7F6E;&#x6587;&#x4EF6;&#x4E2D;&#x5199;&#x76EE;&#x5F55;&#x6700;&#x597D;&#x5199;&#x7EDD;&#x5BF9;&#x76EE;&#x5F55;&#xFF0C;&#x4E0D;&#x8981;&#x5199;&#x76F8;&#x5BF9;&#x76EE;&#x5F55;&#xFF0C;&#x5BB9;&#x6613;&#x62A5;&#x9519;&#xFF01;`**

![](https://img-blog.csdnimg.cn/2020041417204484.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B4eTIwMTU2,size_16,color_FFFFFF,t_70)
说明nginx安装成功。

## 1.2 配置nginx.conf

发现nginx.conf最后一行写着

```
include servers/*;
```

意思是包含servers文件夹下的所有文件，但我并没有找到servers文件夹在哪里，于是手动在/usr/local/etc/nginx中新建一个servers文件夹，放置我们自定义的配置文件，并将最后一行改为

```
include /usr/local/etc/nginx/servers/*;
```

## 1.3 自定义配置文件

然后在servers文件夹下新建一个 `img.happymmall.com.conf`

```
server {
    listen 80;
    autoindex off;
    server_name img.happymmall.com;
    access_log /usr/local/etc/nginx/logs/access.log combined;
    index index.html index.htm index.jsp index.php;
    #error_page 404 /404.html;
    if ( $query_string ~* ".*[\;'\<\>].*" ){
        return 404;
    }

    location ~ /(mmall_fe|mmall_admin_fe)/dist/view/* {
        deny all;
    }

    location / {
        root /ftpfile/img;
        add_header Access-Control-Allow-Origin *;
    }
}
</\>
```

意思是，当在浏览器输入 img.happymmall.com:80 (:80可省略)，请求被转发到 /ftpfile/img文件夹。比如我的/ftpfile/img文件夹下有一个boy.png图片，则访问img.happymmall.com/boy.png应该能看到该图片。

### 设置域名解析

然后还需在 `/etc/hosts`中增加一行

```
127.0.0.1 img.happymmall.com
```

将域名img.happymmall.com的IP地址解析为127.0.0.1。

## 1.4 测试nginx配置文件是否有误

```
sudo nginx -t
```

先检查下配置文件是否正确再启动nginx是个好习惯。

## 1.5 启动nginx

首先我使用的是

```
brew services start nginx
```

来启动。
在浏览器输入 `http://img.happymmall.com/boy.png`
结果发现无法访问

![](https://img-blog.csdnimg.cn/20200414174615301.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B4eTIwMTU2,size_16,color_FFFFFF,t_70)<br> `&#x8FD9;&#x4E2A;&#x95EE;&#x9898;&#x76EE;&#x524D;&#x8FD8;&#x6709;&#x5F85;&#x89E3;&#x51B3;&#x3002;`
先把刚刚启动的nginx关闭。

```
brew services stop nginx
```

换个方式启动nginx。

```
sudo nginx
```

刷新浏览器，结果报403错误了。

# 2. 解决403的问题

## 2.1 更改文件夹权限

首先怀疑是文件夹的权限问题，于是

```
chmod -R 777 /ftpfile/img
```

重启nginx

```
sudo nginx -s reload
```

刷新浏览器，依然403

## 2.2 更改nginx的user

nginx的默认user为nobody（虽然被注释掉了，但仍使用的nobody），但刚刚我们是用root来启动nginx的，可能是用户不统一导致的403。于是把nginx.conf第一行的

```
#user  nobody;
```

改为

```
user  root;
```

测试nginx配置文件

```
sudo nginx -t
```

发现报错：<br> `getgrnam("root") failed in /usr/local/etc/nginx/nginx.conf:2`
百度了下，要把

```
user  root;
```

改为

```
user  root wheel;
```

即要同时指定用户和用户组。改完后测试没问题了，重启nginx，刷新浏览器，再访问 `http://img.happymmall.com/boy.png`真的看到了boy！
![](https://img-blog.csdnimg.cn/20200414181355928.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B4eTIwMTU2,size_16,color_FFFFFF,t_70)
但是访问http://img.happymmall.com仍然会报403，这是因为我们在 `img.happymmall.com.conf`设置了关闭自动索引;

## 2.3 自动索引的使用

在 `img.happymmall.com.conf`中我们设置了

```
autoindex off
```

这样就不能直接访问http://img.happymmall.com，需指定要访问的文件名才能访问，可防止用户穷举文件夹下的所有文件。如果将
autoindex设置为on，则http://img.happymmall.com可访问到 /ftpfile/img文件夹下所有文件。
试一下
在 `img.happymmall.com.conf`中更改

```
autoindex on
```

保存后测试并重启nginx

```
sudo nginx -s reload
```

浏览器访问http://img.happymmall.com
![](https://img-blog.csdnimg.cn/20200414182125643.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B4eTIwMTU2,size_16,color_FFFFFF,t_70)
就不报403了，并可以看到/ftpfile/img文件下下的文件索引。
