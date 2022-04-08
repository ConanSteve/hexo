---
title: zip
date: 2022-02-01 10:00:00
author: ConanSteve
---

### zip

```shell
zip [-dDqrS] [-b path] [zipfile [file ...]]
```

* -d : 从 压缩文件内删除指定的文件

* -D : 压 缩文件内不建立目录名称

* -q : 不显 示指令执行过程

* -r : 递 归处理，将指定目录下的所有文件和子目录一并处理

* -S : 包 含系统和隐藏文件

* -<压缩效率> 压 缩效率是一个介于1-9的 数值

* -b : 创建zip文件临时目录

```bash
zip 
```


### unzip

```shell
unzip [-Z] [-cflptTuvz[abjnoqsCDKLMUVWX$/:^]] file[.zip] [file(s) ...] [-d exdir]
```

* -j : 目录结构不重新创建
* \file[.zip]:待解压的包
* [file(s) …]：要解压的文件，默认解压全部文件
* \ -d : 解压的输出目录,默认当前目录

```
unzip ***.zip
```

