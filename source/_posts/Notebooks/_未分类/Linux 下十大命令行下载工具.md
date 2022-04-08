---
link: https://linux.cn/article-7369-1.html
title: 分享|Linux 下十大命令行下载工具
description: 我们一想到Linux，肯定会想到黑白终端，真正的Linux用户总是偏爱从终端来进行工作，哪怕是用于下载。
keywords: Linux 下十大命令行下载工具
author: null
date: 2016-05-21T01:05:00.000Z
publisher: null
stats: paragraph=114 sentences=1184, words=2108
---
我们一想到Linux，肯定会想到黑白终端，真正的Linux用户总是偏爱从终端来进行工作，哪怕是用于下载。相比某种GUI工具，命令行下载工具可以帮助用户更迅速地从网上下载任何东西。有许多可满足一般用途、甚至用于torrent的下载工具，不过相比其它工具，只有像curl或者wget这少数几款工具更受欢迎。我们在本教程中将探讨用于在Linux环境中下载的十大命令行工具。不妨逐一探讨这些CLI工具。

![](https://img.linux.net.cn/data/attachment/album/201605/21/062101c28s3s4lyc58cs5s.png)

### **1.Wget**

这是最有名的工具，可用于通过CLI下载。这款工具功能很丰富，可以充当某种功能完备的GUI下载管理器，它拥有一款理想的下载管理器所需要的所有功能，比如它可以恢复下载，可以下载多个文件，出现某个连接问题后，可以重新尝试下载，你甚至可以管理最大的下载带宽。

**例子**

从网上下载某个示例文件：

```shell
wget http://www.sample-videos.com/video/mp4/720/big_buck_bunny_720p_1mb.mp4 
```

**示例输出：**

```
--2016-05-11 16:56:23-- http://www.sample- 
 videos.com/video/mp4/720/big_buck_bunny_720p_1mb.mp4 
Resolving www.sample-videos.com (www.sample-videos.com)... 
166.62.28.98 
Connecting to www.sample-videos.com (www.sample- 
videos.com)|166.62.28.98|:80... connected. 
HTTP request sent, awaiting response... 200 OK 
Length: 1055736 (1.0M) 
Saving to: ‘big_buck_bunny_720p_1mb.mp4’ 
100%[==========================================================================================================>] 10,55,736 52.1KB/s in 24s 
2016-05-11 16:56:47 (43.4 KB/s) - ‘big_buck_bunny_720p_1mb.mp4’ saved [1055736/1055736] 
```

后台下载文件：

```shell
wget -b http://www.sample-videos.com/video/mp4/720/big_buck_bunny_720p_1mb.mp4 
```

如果互联网连接出现中断，恢复下载。

```shell
wget -c http://www.sample-videos.com/video/mp4/720/big_buck_bunny_720p_1mb.mp4
```

从某个密码保护的ftp软件库下载文件。

```shell
wget --ftp-user=<user_name> --ftp-password=<Give_password> Download-url-address 
```

### **2.Curl**

Curl是另一种高效的下载工具，它可以用来上传或下载文件，只要使用一个简单的命令。它支持暂停和恢复下载程序包，并支持数量最多的Web协议，可预测下载完成还剩余多少时间，可通过进度条来显示下载进度。它是所有Linux发行版的内置工具。这是一款快速高效的工具，不妨看一下。

**例子：**

```shell
curl -o um.mp4 http://www.sample-videos.com/video/mp4/720/big_buck_bunny_720p_1mb.mp4
```

**示例输出：**

```shell
% Total % Received % Xferd Average Speed Time Time Time Current 
Dload Upload Total Spent Left Speed 
100 1030k 100 1030k 0 0 105k 0 0:00:09 0:00:09 --:--:-- 111k 
```

借助-o选项，提供名称，下载文件会以该名称保存；如使用-O选项，文件就会以原始名称保存。

```shell
curl -O http://www.sample-videos.com/video/mp4/720/big_buck_bunny_720p_1mb.mp4
```

使用一个curl命令，下载多个文件。

```shell
curl -O http://www.sample-videos.com/video/mp4/720/big_buck_bunny_720p_2mb.mp4 -O
```

### **3.Axel**

这是wget的出色替代者，是一款轻量级下载实用工具。它实际上是个加速器，因为它打开了多路http连接，可下载独立文件片段，因而文件下载起来更快速。

**安装**

```shell
apt-get install axel
```

**例子**

```shell
axel http://www.sample-videos.com/video/mp4/720/big_buck_bunny_720p_1mb.mp4 
Initializing download: http://www.sample-videos.com/video/mp4/720/big_buck_bunny_720p_1mb.mp4
```

**示例输出：**

```
File size: 1055736 bytes  
 Opening output file big_buck_bunny_720p_1mb.mp4.0  
 Starting download  
[ 0%] .......... .......... .......... .......... .......... [ 64.9KB/s] 
[ 4%] .......... .......... .......... .......... .......... [ 83.0KB/s] 
[ 9%] .......... .......... .......... .......... .......... [ 91.5KB/s] 
[ 14%] .......... .......... .......... .......... .......... [ 96.8KB/s] 
[ 19%] .......... .......... .......... .......... .......... [ 100.2KB/s] 
[ 24%] .......... .......... .......... .......... .......... [ 102.7KB/s] 
[ 29%] .......... .......... .......... .......... .......... [ 104.6KB/s] 
[ 33%] .......... .......... .......... .......... .......... [ 86.9KB/s] 
[ 38%] .......... .......... .......... .......... .......... [ 77.1KB/s] 
[ 43%] .......... .......... .......... .......... .......... [ 64.8KB/s] 
[ 48%] .......... .......... .......... .......... .......... [ 66.8KB/s] 
[ 53%] .......... .......... .......... .......... .......... [ 72.8KB/s] 
[ 58%] .......... .......... .......... ..... 
Connection 1 finished 
,,,,,,,,,, ,,,,,,,,,, ,,,,,,,,,, ,,,,,..... .......... [ 74.1KB/s] 
[ 63%] .......... .......... .......... .......... .......... [ 79.8KB/s] 
[ 67%] .......... .......... .......... .......... .......... [ 84.5KB/s] 
[ 72%] .......... .......... ..... 
Connection 2 finished 
,,,,,,,,, ,,,,,,,,,, ,,,,,..... .......... .......... [ 86.3KB/s]  
[ 77%] .......... .......... .......... .......... .......... [ 91.6KB/s] 
[ 82%] .......... .......... .......... .......... .......... [ 96.7KB/s] 
[ 87%] .......... .......... .......... .......... .......... [ 101.6KB/s] 
[ 92%] .......... .......... .......... ... 
Connection 0 finished 
,,,,,,,,,, ,,,,,,,,,, ,,,,,,,,,, ,,,....... .......... [ 105.9KB/s]  
[ 96%] .......... .......... .......... 
Downloaded 1031.0 kilobytes in 9 seconds. (108.66 KB/s) 
```

### **4.Youtube-dl**

这是一款专用工具，可以通过命令行从YouTube下载视频，这是个易于安装的程序包，可用来下载一大批文件。

**安装**

```
#&#xA0;curl&#xA0;https://yt-dl.org/latest/youtube-dl&#xA0;-o&#xA0;/usr/local/bin/youtube-dl&#xA0;
```

变更文件权限：

```
#&#xA0;sudo&#xA0;chmod&#xA0;a+rx&#xA0;/usr/local/bin/youtube-dl&#xA0;
```

**例子**

下载一些视频，只要为命令添加视频URL参数。

```
#&#xA0;youtube-dl&#xA0;https://www.youtube.com/watch?v=UZW2hs-2OAI&#xA0;
```

想下载视频列表，将所有URL拷贝到一个文本文件中，然后运行下面这个命令：

1.

```
#&#xA0;youtube-dl&#xA0;-a&#xA0;<name_of_your_text_file.txt>&#xA0;</name_of_your_text_file.txt>
```

**示例输出：**

```
virtual-System-Product-Name&#xA0;prozilla-2.0.4-master&#xA0;#&#xA0;youtube-dl&#xA0;-a&#xA0;url.txt&#xA0;
[youtube]&#xA0;xEf8A7X53YE:&#xA0;Downloading&#xA0;webpage&#xA0;
[youtube]&#xA0;xEf8A7X53YE:&#xA0;Downloading&#xA0;video&#xA0;info&#xA0;webpage&#xA0;
[youtube]&#xA0;xEf8A7X53YE:&#xA0;Extracting&#xA0;video&#xA0;information&#xA0;
[youtube]&#xA0;xEf8A7X53YE:&#xA0;Downloading&#xA0;MPD&#xA0;manifest&#xA0;
[download]&#xA0;Destination:&#xA0;EIC&#xA0;Outrage&#xA0;-&#xA0;Salute&#xA0;to&#xA0;Indian&#xA0;Athletes!-xEf8A7X53YE.mp4&#xA0;
[download]&#xA0;3.9%&#xA0;of&#xA0;70.87MiB&#xA0;at&#xA0;82.53KiB/s&#xA0;ETA&#xA0;14:04&#xA0;
```

### **5.Aria2**

这是一种开源命令行下载加速器，支持多个端口，你可以使用最大带宽来下载文件，是一款易于安装、易于使用的工具。

**安装**

```
#&#xA0;apt-get&#xA0;install&#xA0;aria2&#xA0;
### &#x9488;&#x5BF9;centOS&#xA0;
#&#xA0;yum&#xA0;install&#xA0;aria2
```

**例子**

```
#&#xA0;aria2c&#xA0;http://www.sample-videos.com/video/mp4/720/big_buck_bunny_720p_1mb.mp4
```

**示例输出：**

```
[#28c7dd&#xA0;0.9MiB/1.0MiB(93%)&#xA0;CN:1&#xA0;DL:70KiB&#xA0;ETA:1s]&#xA0;
05/11&#xA0;23:06:47&#xA0;[NOTICE]&#xA0;Download&#xA0;complete:&#xA0;
/home/virtual/Desktop/prozilla-2.0.4-master/big_buck_bunny_720p_1mb.mp4&#xA0;
Download&#xA0;Results:&#xA0;
gid&#xA0;|stat|avg&#xA0;speed&#xA0;|path/URI&#xA0;
======+====+===========+=======================================================&#xA0;
28c7dd|OK&#xA0;|&#xA0;72KiB/s|/home/virtual/Desktop/prozilla-2.0.4-master/big_buck_bunny_720p_1mb.mp4&#xA0;
Status&#xA0;Legend:&#xA0;
(OK):download&#xA0;completed.

```

### **6.Movgrab**

这是用于下载视频的另一款高效工具，使用movgrab的优点在于，它不仅可以从YouTube下载视频，还可以从几乎所有的知名网站下载视频，比如metacafe、dailiymotion、 ehow和vobx等。这是一款很快速的工具，可以定义影片格式，还可以恢复下载。

**安装**

可以从该[链接](https://01c3c482-a-62cb3a1a-s-sites.googlegroups.com/site/columscode/files/movgrab-1.2.1.tar.gz?attachauth=ANoY7co3CB5Bhn675vOfjy3OKCJADnh9oqY4HjyZfm2AwuidRnepaU_6CyWNZlHw1oNkOZSsTX02pr-Yr_EiV45-w0mI-ycWtiXDeB81F5Lhf3yMrG2wXiVk8ixeQt_9jsdgJrGlnaPnBnBzR95ViakwzW1CS3yUKt2ojsCMYb_irKNokYCBv2IsSIsfSyKtrb-ldnakhj5jqpTEKtc-Cbg7o_58hM3vgnf9IqeBvP1C3LMFeBmKJuQ%3D&attredirects=0)下载程序包。

解压缩程序包：

```
#&#xA0;tar&#xA0;-xvf&#xA0;movgrab-1.2.1.tar.gz&#xA0;
#&#xA0;cd&#xA0;movgrab-1.2.1&#xA0;
#&#xA0;./configure&#xA0;
#&#xA0;make&#xA0;
#&#xA0;make&#xA0;install
```

使用命令下载程序包

下载名称指定的文件：

```
#&#xA0;movgrab&#xA0;Youtube_url&#xA0;
```

指定输出文件：

```
#&#xA0;movgrab&#xA0;-o&#xA0;example.mp4&#xA0;video_url&#xA0;
```

使用maovgrab –h，即可了解更多的细节。

### **7.rtorrent**

这种知名的命令行torrent客户软件随附在所有Linux发行版中，它需要screen实用工具才能正常运行。

**安装**

安装screen：

```
#&#xA0;apt-get&#xA0;install&#xA0;screen&#xA0;
```

安装rtorrent ：

```
#&#xA0;apt-get&#xA0;install&#xA0;rtorrent&#xA0;
```

例子

```
#&#xA0;rtorrent&#xA0;example.torrent
```

![](https://img.linux.net.cn/data/attachment/album/201605/21/062110zixx0nzinq31r03s.jpg)

### **8.ctorrent**

C-torrent是最简单的命令行torrent下载工具，可以迅速安装，也是micro-torrent或utorrent的优秀替代者。

**安装**

```
#&#xA0;apt-get&#xA0;install&#xA0;ctorrent&#xA0;
```

**例子**

我们不妨下载一份最新版本的Ubuntu server 16.04。

```
#&#xA0;ctorrent&#xA0;ubuntu-16.04-server-amd64.iso.torrent
```

![](https://img.linux.net.cn/data/attachment/album/201605/21/062110f76uvduj6d269xxo.jpg)

使用ctorrent –h，即可了解更多选项。

### **9.Transmission-cli**

Transmission的这个命令行版本是一款非常强大的工具，可用于下载torrent。易于安装，它需要screen这个依赖项。

**安装**

```
#&#xA0;apt-get&#xA0;install&#xA0;transmission-cli&#xA0;transmission-daemon&#xA0;transmission-common&#xA0;
```

安装screen

```
#&#xA0;apt-get&#xA0;install&#xA0;screen&#xA0;
```

**例子**

```
#&#xA0;screen&#xA0;-a&#xA0;/usr/bin/transmission-cli&#xA0;-p&#xA0;25000&#xA0;ubuntu-16.04-server-amd64.iso.torrent
```

![](https://img.linux.net.cn/data/attachment/album/201605/21/062110z55iz6nppd3nohag.jpg)

### **10.vuze**

这是一种全面的torrent下载解决方案，占用资源极少，是功能最强大的torrent应用程序之一，它需要Java才能在控制台上运行，所以确保你已将open jdk的jre安装到系统上，它同样需要screen程序包。

**安装**

可以直接从该[链接](http://www.vuze.com/download.php)下载，下载后解压缩程序包。

```
#&#xA0;tar&#xA0;-xvf&#xA0;VuzeInstaller.tar.bz2&#xA0;&#xA0;
#&#xA0;cd&#xA0;vuze
```

有一些依赖项必须下载，从该[链接](http://svn.vuze.com/public/client/trunk/uis/lib/)获取必要的插件。

将这些.jar插件拷贝到vuze目录：

```
#&#xA0;cp&#xA0;*.jar&#xA0;vuze&#xA0;
```

运行下面这个命令：

```
#&#xA0;java&#xA0;-cp&#xA0;"Azureus2.jar:commons-cli.jar:log4j.jar"&#xA0;org.gudy.azureus2.ui.common.Main&#xA0;--ui=console
```

上述命令成功执行后，运行下面这个命令来启动

```
#&#xA0;screen&#xA0;java&#xA0;-jar&#xA0;Azureus2.jar&#xA0;--ui=console
```

![](https://img.linux.net.cn/data/attachment/album/201605/21/062110vc6vmc6dibci8chz.jpg)

使用help命令，给add命令添加上.torrent文件的路径，即可开始下载。

![](https://img.linux.net.cn/data/attachment/album/201605/21/062111tss8wlvrp0d9kkvd.jpg)

### **结束语**

相比基于GUI的torrent或下载管理器，命令行工具来得更高效而快速。这些工具在无外设服务器中扮演重要角色，可以控制慢速互联网连接中的带宽使用。

请尽情享用！
