---
title: 在Mac上通过imagemagick压缩gif动图
date: 2022-04-11
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
categories: Mac

---

# 安装homebrew

参照网络

# 安装imagemagick

```shell
brew install imagemagick
```

# 转换

终端里输入：

```shell
convert old.gif -fuzz 15% -layers Optimize new.gif
```

(-fuzz 15%指压缩率15%，你也可以尝试换成别的数值 ， newlsj.gif代表压制后动图的文件名，你可以随便改成别的)