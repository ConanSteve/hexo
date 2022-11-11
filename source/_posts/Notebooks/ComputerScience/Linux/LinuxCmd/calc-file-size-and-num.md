---
date: 2022-03-30T19:43:00
title: 终端统计文件夹信息
author: 陌上人如玉
categories: [Linux, Linux命令]
tags: linux
---

`wc`命令参数

* -l：仅列出行

### 统计文件夹数量

包括子目录

```shell
find ./ -type d |wc -l
```

