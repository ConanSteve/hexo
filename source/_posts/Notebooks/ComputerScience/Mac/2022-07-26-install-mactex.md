# Macos 安装MacTex

## [下载地址](http://ftp.math.utah.edu/pub/tex/historic/systems/mactex/)


所以很多老师都要求学生用Latex来写论文。那么问题来了，latex要在哪里写？有像word一样的编辑器吗？答案是肯定的。市面上的latex编辑器不下20种，各种系统都有，常见的有：LyX、TeXworks、TexStudio、WinEdt、Emacs、Sublime Text、Atom、Visual Studio Code

本文将介绍如何在mac系统下，用sublime配置latex环境。

准备软件
MacTex Latex运行的必备环境，可用[清华镜像Index of /ctan/systems/mac/mactex/ | 清华大学开源软件镜像站 | Tsinghua Open Source Mirror](https://mirrors.tuna.tsinghua.edu.cn/ctan/systems/mac/mactex/)
[Sublime Text 编辑器](https://xclient.info/s/sublime-text.html?_=4847db8d4fcfc9682f3ac7932c81436e)，写代码的应该都很熟悉（这个地址是破*解&版的福利哦）
[Skim PDF](https://sourceforge.net/projects/skim-app/files/Skim/Skim-1.4.26/Skim-1.4.26.dmg/download)阅读器，有它你才能预览你的文档

安装步骤
首先下载MacTex安装，傻瓜式安装。MacTex文件比较大，有4G+，介意的话可以选择MacTex_Basic包，只有是100M以内，但是如果安装MacTex_Basic，后期可能会遇到各种缺包的问题。

第二步安装Sublime Text 3。安装好后，安装插件LaTexTool。具体步骤如下：

2.1 安装 Package Control
打开 Sublime Text 3 选择 Tools，选择 Install Package Control…（需要科学上网）

 在Sublime Text -> Peference 选择Package Control，输入Install Package

输入LaTeXTools ，回车安装 LaTeXTools 插件。
安装Skim
安装好后运行Skim，进入Skim——选项，点击同步进行设置


勾选检查文件变化、自动重新加载，在PDF-Tex同步支持那里选择sublime Text，这样当你编译tex后就会自动打开pdf预览了。
完成上面所有步骤，latex基本环境就搭建好了。下面可以测试一下。
创建一个test.tex文档，复制以下内容粘贴到Sublime Text3文档中：
```latex
%!TEX program = xelatex
\documentclass{article}
\usepackage{fontspec, xunicode, xltxtra}
\setmainfont{Hiragino Sans GB}
\title{Title}
\author{}
\begin{document}
\maketitle{}
\section{Introduction}
This is where you will write your content. 在这里写上内容。
\end{document}
```
保存以后，按下 command⌘ + B进行编译选择Latex ，如果以上操作无误，下面会提示Build completed，然后 Skim 弹出 PDF 预览。

番外篇
完成上面的步骤，基本上可以正常编写文档了，但是如果你写的是中文文档，那事情可就还没结束，还完成以下的配置才能开心地编写中文文档。打开终端，运行：
```
sudo tlmgr update --self
sudo tlmgr install latexmk
```
在sublime Text里打开LaTeXTools.sublime-settings（也就是LaTeXTools的用户设置，如果你是从旧版本升级上来或者担心这个配置文件出现问题，可以依次点击Preferences——Package Settings——LaTeXTools——Reconfigure LaTeXTools and migrate settings重建配置文件），在builder-settings下面新增两项配置：
```
"program" : "xelatex",
"command" : ["latexmk", "-cd", "-e", "$pdflatex = 'xelatex -interaction=nonstopmode -synctex=1 %S %O'", "-f", "-pdf"],
```
另外注意之前应该有"builder": "default"（或直接设置为空或”traditional”）。

保存配置文件后关闭，重新编译一下，即可正常显示中文。

Tips
如果你忘记公式的代码，可以用这个LaTex公式编辑器：http://private.codecogs.com/latex/eqneditor.php

如果你测试的时候遇到如下错误：
```
File "/Users/huwei/Desktop/test.tex", line 1
%!TEX program = xelatex
^
SyntaxError: invalid syntax
```
那可能是你sublime Text的默认编译环境被设置为python了，可以点击Tools->Build System，将其设置为Automatic，这样编辑器就会根据文件的后缀来自动识别文件类型了。

# Reference
1. [Macos 安装MacTex SublimeText3 Skim环境](https://blog.csdn.net/u012149181/article/details/121961875)
2. [macOS + Sublime Text + Latex 环境配置](https://www.jianshu.com/p/50a813c8a6ea)
3. [Mac安装与使用MacTeX](https://blog.csdn.net/ChrisP_333/article/details/82943508)