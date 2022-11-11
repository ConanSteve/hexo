---
title: 通过zip命令压缩和解压缩文件
date: 2022-04-15 10:00:00
author: ConanSteve
categories: [Linux, Linux命令]
---

通常 zip 已经安装，但验证下也没坏处。你可以运行以下命令来安装 `zip` 和 `unzip`。如果它尚未安装，它将立即安装。

```bash
sudo apt install zip unzip
```

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
zip -r output_file.zip file1 folder1
# 如果文件过大，建议不显示指令执行过程
zip -qr output_file.zip file1 folder1
```

分卷压缩和合并解压

```shell
# ----- 分卷压缩 -----
 
# 将文件或者文件件打包为zip压缩包，book.zip大小为38.8M
zip -r book.zip ./input.pdf
# 将book.zip分割，每个压缩包不超过20M，生成两个压缩包subbook.zip（17.8M）和subbook.z01（21M）
zip -s 20m book.zip --out subbook.zip
 
 
# ----- 合并解压 -----
 
# 将上述两个压缩包合并为一个压缩文件single.zip
zip subbook.zip -s=0 --out single.zip
# 解压single.zip
unzip -d ./ single.zip
```



### unzip

```shell
unzip [-Z] [-cflptTuvz[abjnoqsCDKLMUVWX$/:^]] file[.zip] [file(s) ...] [-d exdir]
```

* -j : 目录结构不重新创建
* file[.zip]:待解压的包
* [file(s) …]：要解压的文件，默认解压全部文件
* -d : 解压的输出目录,默认当前目录

```
unzip ***.zip
```

### zipsplit

命令用于将较大的“zip”压缩包分割成各个较小的“zip”压缩包。

**语法格式：**zipsplit [参数]

**常用参数：**

| -n   | 指定分割后每个zip文件的大小       |
| ---- | --------------------------------- |
| -t   | 报告将要产生的较小的zip文件的大小 |
| -b   | 指定分割后的zip文件的存放位置     |

**参考实例**

分割每个文件为1k：

```shell
zipsplit -n 1000 file.zip 
```

指定分割后的zip文件的存放位置：

```shell
zipsplit -b 50 file.zip file1
```



# Reference

1. [初级：如何在 Linux 中 zip 压缩文件和文件夹](https://linux.cn/article-10778-1.html)
