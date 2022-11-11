---
title: Mac安装Homebrew
date: 2022-02-01 10:00:00
author: 陌上人如玉
categories: Mac
tags: mac
---

# 安装homebrew

```shell
# 已废弃
/usr/bin/ruby -e "$(curl -fsSL https://cdn.jsdelivr.net/gh/ineo6/homebrew-install/install)"
# 建议
/bin/bash -c "$(curl -fsSL https://gitee.com/ineo6/homebrew-install/raw/master/install.sh)"

# 查看当前源
cd "$(brew --repo)" && git remote -v

# 设置中科大镜像
git -C "$(brew --repo)" remote set-url origin https://mirrors.ustc.edu.cn/brew.git
git -C "$(brew --repo homebrew/core)" remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git

# 设置清华镜像
git -C "$(brew --repo)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git
```

# 卸载
```
/bin/bash -c "$(curl -fsSL https://gitee.com/ineo6/homebrew-install/raw/master/uninstall.sh)"

```

# Reference

* [如何安装homebrew](https://cloud.tencent.com/developer/article/1853162)

* [配置环境变量](https://blog.csdn.net/sinat_38184748/article/details/114115441)

* [M1芯片的MacOS 上安装wget的具体过程-图文教程](https://blog.csdn.net/NBDwo/article/details/121322116)

* [清华镜像安装](https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/)
* [**Homebrew更换国内镜像源（中科大、阿里、清华）**](https://blog.csdn.net/H_WeiC/article/details/107857302)