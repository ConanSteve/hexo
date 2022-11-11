---
title: SSH
date: 2022-02-01 10:00:00
author: ConanSteve
---

## 自动生成key

* linux/mac： 
> `ssh-keygen -t rsa`            
> `ssh-keygen -t rsa -b 4096 `
* windows：
> `ssh-keygen.exe -t rsa`

## 拷贝key到主机

linux:

```
ssh-copy-id -i  "key_path"  "user_name"``@ip_address
ssh-copy-id -i .ssh/id_rsa.pub zhangfan@172.18.32.92
```

# Reference

1. [vscode remote ssh 多重跳接配置内网穿透](https://blog.csdn.net/qq_38476684/article/details/100028507)

2. [vscode通过跳板机(堡垒机)连接remote服务器](https://blog.csdn.net/dcz1994/article/details/103120254?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromBaidu-1.control&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromBaidu-1.control)