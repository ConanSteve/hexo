---
title: 通过hexo搭建个人博客
date: 2022-04-01 10:00:00
author: 陌上人如玉
comments:
description:
keywords:
top_img:
cover:
mathjax:
katex:
aside: false
aplayer:
highlight_shrink:
tags: 
categories:
---

# Hexo



## 搭建自己的个人博客总体来说有三种选择

### 1. 使用现有的

现在市面上的博客有很多，如CSDN，博客园，简书等平台。都可以直接在上面发表自己的博客，用户交互也做的很好，写的文章在各大搜索引擎下也能搜索的到，比如百度、搜狗等。但是缺点是不太自由，会受到平台的各种限制和很多烦人的广告。

### 2. 自己购买域名和服务器

这种方式搭建博客的成本比较高，购买成本，还有花费力气自己搭这么一个网站，并且需要定期的维护它，对于我们大多数人来说，实在是没有这样的精力和时间。

### 3. 使用GitHub Page平台

第三种选择，直接在GitHub Page平台上托管我们的博客。这样就可以安心的来写作，又不需要定期维护，而且hexo作为一个快速简洁的博客框架，用它来搭建博客真的非常容易。

## 本教程分三个部分

本教程大部分是通过网络进行收集，并结合我个人的一些理解编写的。

* 第一部分：hexo的搭建并部署到GitHub Page上，以及个人域名的绑定。
* 第二部分：hexo的基本配置，更换主题，实现多终端工作，以及在coding page部署实现国内外分流
* 第三部分：hexo添加各种功能，包括搜索的SEO，阅读量统计，访问量统计和评论系统等。

## 第一部分

hexo的搭建并部署到GitHub Page上，以及个人域名的绑定。

### hexo 简介

hexo是一款基于Node.js的静态博客框架，依赖少易于安装使用，可以方便的生成静态网页托管在GitHub和Coding上，是搭建博客的首选框架。大家可以进入[hexo官网](https://hexo.io/)进行详细查看，因为Hexo的创建者是台湾人，对中文的支持很友好，可以选择中文进行查看。

### Hexo搭建步骤

1. 安装Git
2. 安装Node.js
3. 安装Hexo
4. GitHub创建个人仓库
5. 生成SSH添加到GitHub
6. 将hexo部署到GitHub
7. 设置个人域名
8. 发布文章

#### 1. 安装Git

Git是目前世界上最先进的分布式版本控制系统，可以有效、高速的处理从很小到非常大的项目版本管理。也就是用来管理你的hexo博客文章，上传到GitHub的工具。Git非常强大，我觉得建议每个人都去[Git官网](https://git-scm.com/)了解一下。

* windows：到git官网上下载，[Download git](https://git-scm.com/downloads)，下载后会有一个Git Bash的命令行工具，以后就用这个工具来使用git。
* linux：对linux来说实在是太简单了，因为最早的git就是在linux上编写的，只需要一行代码。

```shell
sudo apt-get install git
```

安装好后，用 `git --version` 来查看一下版本

#### 2. 安装nodejs

Hexo是基于nodeJS编写的，所以需要安装一下nodeJs和里面的npm工具。

* windows：nodejs选择LTS版本就行了。[node.js LTS Download](https://nodejs.org/en/download/)
* linux：

```shell
sudo apt-get install nodejs
sudo apt-get install npm
```
* macOS
```shell
brew install nodejs
brew install npm
```


安装完后，打开命令行查看版本。

```shell
node -v
npm -v
```

检查一下有没有安装成功

顺便说一下，windows在git安装完后，就可以直接使用git bash来敲命令行了，不用自带的cmd，cmd有点难用。

#### 3. 安装hexo

前面git和nodejs安装好后，就可以安装hexo了，你可以先创建一个文件夹blog，然后cd到这个文件夹下（或者在这个文件夹下直接右键git bash打开）。

输入命令

```shell
npm install -g hexo-cli
# macOS也可以通过homebrew安装
brew install hexo
```

依旧用 `hexo -v`查看一下版本

至此hexo的环境就部署完了。

接下来初始化一下hexo

```shell
hexo init myBlog
```

这个myBlog可以自己取什么名字都行，然后

```shell
cd myBlog //进入这个myBlog文件夹npm install
```

新建完成后，文件夹目录下有：

* node_modules: 依赖包
* public：存放生成的页面
* scaffolds：生成文章的一些模板
* source：用来存放你的文章
* themes：主题
* _config.yml：config.yml: 博客的配置文件

启动hexo服务

```shell
hexo g && hexo server
```

打开hexo的服务，在浏览器输入localhost:4000 就可以看到你生成的博客了。

使用ctrl+c可以把服务关掉。

#### 4. GitHub创建个人仓库

首先，你先要有一个GitHub账户，没有请注册。[GitHub官网](https://github.com/)

注册完登录后，在GitHub.com中看到一个New repository，新建仓库

创建一个和你用户名相同的仓库，后面加.github.io，比如你注册的用户名叫 zhangsan，那么你创建的仓库名就叫 zhangsan.github.io，只有这样，将来要部署到GitHub Page的时候，才会被识别，也就是xxxx.github.io，其中xxx就是你注册GitHub的用户名。

点击create repository。

#### 5. 生成SSH添加到GitHub

回到你的git bash中。

```shell
git config --global user.name "yourname"git config --global user.email "youremail"
```

这里的yourname输入你的GitHub用户名，youremail输入你GitHub的邮箱。这样GitHub才能知道你是不是对应它的账户。

可以用以下两条，检查一下你有没有输对

```shell
git config user.namegit config user.email
```

然后输入下面的命令，创建SSH,一路回车就可以了。

```shell
ssh-keygen -t rsa -C "youremail"
```

这个时候它会告诉你已经生成了.ssh的文件夹。在你的电脑中找到这个文件夹。

ssh，简单来讲，就是一个秘钥，其中，id_rsa是你这台电脑的私人秘钥，不能给别人看的，id_rsa.pub是公共秘钥，可以随便给别人看。把这个公钥放在GitHub上，这样当你链接GitHub自己的账户时，它就会根据公钥匹配你的私钥，当能够相互匹配时，才能够顺利的通过git上传你的文件到GitHub上。

而后在GitHub的setting中，找到SSH keys的设置选项，点击New SSH key
把你的id_rsa.pub里面的信息复制进去。

在gitbash中，查看是否成功

```
ssh -T git@github.com
```

#### 6. 将hexo部署到GitHub

这一步，我们将hexo和GitHub关联起来，也就是将hexo生成的文章部署到GitHub上，打开站点配置文件_config.yml，翻到最后，修改为
YourgithubName就是你的GitHub账户

```
deploy:  type: git  repo: https://github.com/**YourgithubName**/**YourgithubName**.github.io.git  branch: master
```

这个时候需要先安装deploy-git ，也就是部署的命令,这样你才能用命令部署到GitHub。

```
npm install hexo-deployer-git --save
```

然后输入

```shell
hexo clean
hexo g
hexo d
```

其中 hexo clean清除了你之前生成的东西，也可以不加。
hexo generate 顾名思义，生成静态文章，可以用 hexo g缩写
hexo deploy 部署文章，可以用hexo d缩写
此处命令可以用一条命令代替，然后等它全部执行完就部署到网站上了，不用在哪里等着输下一条命令

```
hexo clean && hexo g && hexo d
```

注意：第一次使用deploy时会让你你输入GitHub的username和password。

得到下图就说明部署成功了，过一会儿就可以在[http://yourname.github.io](http://yourname.github.io) 这个网站看到你的博客了！！

#### 7. 设置个人域名

现在你的个人网站的地址是 yourname.github.io，如果觉得这个网址逼格不太够，这就需要你设置个人域名了。但是需要花钱。

注册一个阿里云账户,在阿里云上买一个域名，我买的是 fangzh.top，各个后缀的价格不太一样，比如最广泛的.com就比较贵，看个人喜好咯。

你需要先去进行实名认证,然后在域名控制台中，看到你购买的域名。

点解析进去，添加解析。

其中，192.30.252.153 和 192.30.252.154 是GitHub的服务器地址。
注意，解析线路选择默认，不要像我一样选境外。这个境外是后面来做国内外分流用的,在后面的博客中会讲到。记得现在选择默认！！

登录GitHub，进入之前创建的仓库，点击settings，设置Custom domain，输入你的域名fangzh.top

然后在你的博客文件source中创建一个名为CNAME文件，不要后缀。写上你的域名。

最后，在gitbash中，输入

```shell
hexo clean && hexo g && hexo d
```

过不了多久，再打开你的浏览器，输入你自己的域名，就可以看到搭建的网站啦！

接下来你就可以正式开始写文章了。

```shell
hexo new newpapername
```

然后在source/_post中打开markdown文件，就可以开始编辑了。当你写完的时候，再更新一下。

```shell
hexo clean && hexo g && hexo d
```

就可以看到更新了。

#### 8. 其他设置

指定服务器端口

```shell
hexo server -p 5000
```

## 第二部分
### 如何更新butterfly主题
1、先将主题备份
2、然后执行`npm update butterfly`
3、使用`BeyondCompare`软件比较两个`_config.yaml`文件，将不同的部分从旧文件转移到新配置。
4、将原主题的`source\img`文件夹的内容拷贝进入新版本主题当中。

> 预计花费10分钟左右

### 问题处理
* 报错`hexo Database load failed. Deleting database`
> 把这个根目录下的 node_modules 和 package-lock.json 给删掉，再执行一下 npm install，之后发现问题得到解决。



# 总结

教程总体来说还是比较简单的，用心花费点时间就能搭建好。当然如果你有什么不理解的，可以通过在线聊天找到我！

# Reference

1. [使用Hexo搭建博客](http://hekun97@github.io/2020/02/16/shi-yong-hexo-da-jian-zi-ji-de-ge-ren-bo-ke-yi/index.html)