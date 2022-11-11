---
link: https://blog.csdn.net/Hanghang_/article/details/78944672
title: 使用github+jekyll一小时搭建个人博客（小白专用）
description: 很早就听过github的大名，但一直不知道github是什么，只知道别人会把他们的代码放上去。那就在这里简单介绍一下github。百度是这样说的： gitHub是一个面向开源及私有软件项目的托管平台，因为只支持git 作为唯一的版本库格式进行托管，故名gitHub。可能大家觉得还是不懂是干什么的，没错，看到这句话的时候我也不懂它是干嘛的，经过半天的学习，我了解到： 首先，github是一个版本管
keywords: jekyll搭建个人博客
author: Hecttttttttt Csdn认证博客专家 Csdn认证企业博客 码龄5年 暂无认证
date: 2018-01-01T02:08:20.000Z
publisher: null
stats: paragraph=29 sentences=40, words=77
---
很早就听过github的大名，但一直不知道github是什么，只知道别人会把他们的代码放上去。那就在这里简单介绍一下github。

**百度是这样说的：**
gitHub是一个面向开源及私有软件项目的托管平台，因为只支持git 作为唯一的版本库格式进行托管，故名gitHub。

可能大家觉得还是不懂是干什么的，没错，看到这句话的时候我也不懂它是干嘛的，经过半天的学习，我了解到：
**首先，github是一个版本管理器。**当你在做一个项目时，你可以每做一次修改就保存一次版本，当你想回退到某一版本时，就可以很方便地回退了。
**其次，github为开源项目的改进做了很大贡献。 **我们可以把一些开源的项目拿来自己用，也可以加以修改，这样一个开源的项目经过别人的无数次修改，就会变得更好。**
**再有就是，github使多人开发更加方便**，做一个项目的时候，可以把项目的管理权限分发给一起做项目的小伙伴，然后大家就都可以编辑这个项目啦！是不是很方便呢

以上的说法不是很官方，因为我也是刚学，还没有真正实战，如果说的不对请各位大神指出。

说了那么久的github，这两天突然心血来潮，突然想建立一个属于自己的个人博客，通过搜索了很多资料，发现一个免费而又简单的搭建博客的方法。就是 **利用github下面的github pages+jekyll一个简单的免费的Blog生成工具**。

*github pages 主页 https://pages.github.com/ *
_jekyll中文网站 主页 https://www.jekyll.com.cn/_
_我的博客主页 https://hectoor.github.io/_

### **步骤一：注册一个github**

![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTgwMTAxMTAxMDIzMzgy?x-oss-process=image/format,png)
输入昵称邮箱密码注册。

### **步骤二：前往jekyll的主题商店挑选主题**

主题商店：http://jekyllthemes.org/
![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTgwMTAxMTAyOTQ2NjMy?x-oss-process=image/format,png)
**挑一个你喜欢的点击**
![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTgwMTAxMTAzMDM0MjUz?x-oss-process=image/format,png)
**点击Homepage**
### **步骤三：fork别人的项目**
![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTgwMTAxMTAzMTMyMjA1?x-oss-process=image/format,png)
**点击Fork**
![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTgwMTAxMTAzNjExNjI2?x-oss-process=image/format,png)
**转到Settings，然后修改项目名字**

#### **如果没有意外，这个时候你就可以打开你的个人博客了，地址是： 你的github名字.github.io，如我的github名字是Hectoor，则我的个人博客是Hectoor.github.io，但是里面的信息还是别人的**

### **步骤四:在电脑上修改文件配置**
修改完之后，转到Code，此时需要借助一个软件，github 的桌面软件，方便你更好的上传代码。

_github for windows https://desktop.github.com/_
下载完成后

![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTgwMTAxMTA1NDIwNDkw?x-oss-process=image/format,png)
**系统会自动打开这个软件**
![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTgwMTAxMTA1NTM2MjM4?x-oss-process=image/format,png)

#### **打开路径，然后选择使用Notepad++（一个很好用的文本编辑器，可以打开很多格式的文件）打开_config.yml这个文件，其中博客的一些基本配置会在这里，需要修改**

_Notepad++下载地址：https://notepad-plus-plus.org/_

![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTgwMTAxMTA1NjE0OTQ2?x-oss-process=image/format,png)

**现在我们的博客还是完完整整地克隆别人的，我们当然希望修改主页面上的信息，例如博客名，等等。现在我们用打开的_config.yml和博客页面对比一下，你就大概知道需要改哪些东西了**
![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTgwMTAxMTEwODM1MjQy?x-oss-process=image/format,png)
**修改之后点击左上角的保存，然后打开github for windows **

![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTgwMTAxMTEyMTI1ODQ5?x-oss-process=image/format,png)

![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTgwMTAxMTEyMTUyNDY0?x-oss-process=image/format,png)

####这个时候你再去看看你的主页，就发现基本信息（博客名之类）改得差不多了，如果发现不满意，还可以回退之前的版本，这里就不说了。
### **步骤五：开始写博客**

博客的文件是放在项目的**_posts**文件中的，这里要注意文件名称的格式， **年-月-日-文章标题.markdown** ，一般我们是用markdown编写文章，这种编辑方式也是非常的方便。如果还不知道markdown怎么使用的同学，可以参考

_认识与入门：markdown ：https://sspai.com/post/25137_

可以参考我博客中的**_posts **中的**2017-12-31-my-first-blog.markdown**

**修改之后，保存，回到github for windows上创建新版本，上传版本，此处与步骤四相同。**

#### **参考文档**
http://playingfingers.com/2016/03/26/build-a-blog/
http://kresnik.wang/works/tech/2015/06/07/%E5%9C%A8github-pages%E7%BD%91%E7%AB%99%E4%B8%8B%E7%94%A8jekyll%E5%88%B6%E4%BD%9C%E5%8D%9A%E5%AE%A2%E6%95%99%E7%A8%8B.html
http://www.chinaz.com/web/2014/0616/355745_2.shtml

恭喜你，成功了！！！哦不，还差一步，不评论关注一下我？![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTgwMTAxMTMxMTA3ODU0?x-oss-process=image/format,png)

我的github：https://github.com/Hectoor

> 如果我的文章对你有帮助，欢迎关注，点赞，收藏.
