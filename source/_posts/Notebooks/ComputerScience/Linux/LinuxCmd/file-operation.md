---
title: Linux常见文件操作命令
date: 2022-04-15T16:00:00
author: 陌上人如玉
comments:
description: linux复制、重命名文件和文件夹
keywords:
top_img:
cover:
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
tags: linux
hide: true
categories:
  [Linux, Linux命令]
---

## 文件复制拷贝删除

```shell
cp -i a.c /path/a.c # copy file
rm -rf a.py　   # 删除文件
rm -rf data     # 删除文件夹 
touch a.py/vim a.py      # 创建文件
mkdir data      # 创建文件夹
scp /home/lmc/a.py(local) username@ip:/home/lmc/fuwuqi/(remote)  # copy单个文件到远程
scp -r /home/lmc/test/ xxx@192.168.x.xxx:/home/lmc/fuwuqi/   # copy文件夹到远程
```

## 文件查找

[查找软件安装位置](https://blog.csdn.net/faihung/article/details/84101603)

```
find / -name nginx
find . -name "*libc*"
```

用于查找文件里符合条件的字符串 `grep`
[查看版本信息](https://blog.51cto.com/nameyjj/557424) `lsb_release -a` 
[终端下载文件](https://www.linuxprobe.com/five-command-down-browse.html)
配置环境变量

```
 vim ~/.bashrc
 export PATH="你的路劲/anaconda3/bin:$PATH"
```

查看文件夹下文件内容所在位置： `grep -r "api/v2"`

查找当前用户监听端口

`lsof -i |grep LISTEN`

## 移动文件或文件夹

```shell
mv 旧文件/目录 新文件名/目录
```

## 重命名文件或文件夹

```shell
mv oldName newName 
```

