---
title: 终端工具配置
date: 2022-02-01 10:00:00
author: ConanSteve
---

# 终端工具配置

# zsh安装

如果你用 Mac，就可以直接看下一节

如果你用 Redhat Linux，执行：`sudo yum install zsh`

如果你用 Ubuntu Linux，执行：`sudo apt-get install zsh`

如果你用 Windows……去洗洗睡吧。

安装完成后设置当前用户使用 zsh：`chsh -s /bin/zsh`，根据提示输入当前用户的密码就可以了。

# oh-my-zsh

oh-my-zsh可能会影响速度，所以，可以不安装，如果不安装，插件的安装，建议使用”一步安装“

安装「oh my zsh」可以自动安装也可以手动安装。

自动安装：

```Bash
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
```


手动安装：

```Bash
git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
```


都不复杂，安装完成之后退出当前会话重新打开一个终端窗口，你就可以见到这个彩色的提示了：

![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011530511.png)

**默认推荐配置**

```shell
export ZSH="$HOME/.oh-my-zsh"
ZSH_THEME="robbyrussell"
source $ZSH/oh-my-zsh.sh
plugins=(git history vscode sublime sudo)
```



# 主题安装

## Powerlevel10k

官网：[https://github.com/romkatv/powerlevel10k](https://github.com/romkatv/powerlevel10k)

可以选择pure主题

```Bash
git clone --depth=1 https://gitee.com/romkatv/powerlevel10k.git ~/.zsh/plugins/powerlevel10k
echo 'source ~/.zsh/plugins/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
source ~/.zshrc
```

### p10k configure

### [安装Hack Nerd字体](https://www.nerdfonts.com/font-downloads)

### VSCode字体设置

```nginx
Hack Nerd Font Mono, Monaco, 'Courier New', monospace
```


## Pure

官网：[https://github.com/sindresorhus/pure](https://github.com/sindresorhus/pure)

建议通过使用Powerlevel10k安装

```Bash
brew install node
brew install pure
git clone https://gitee.com/URmyLucky/pure2020.git ~/.zsh/plugins/pure
echo "source ${(q-)PWD}/.zsh/plugins/pure/pure.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc
source ~/.zshrc
```


.zshrc文件中添加

```text
autoload -U promptinit; promptinit
prompt pure
```


# 必备插件安装

## 安装自动补全功能

### 方法一

使用 `zsh` 我认为第一个吸引我的重要插件就是 [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)。它会自动为你的终端命令提供补全建议，让你能更加快速的完成命令输入，有了它，你再也不用一遍遍的按 `tab` 来加快你的命令输入了。

`zsh-autosuggestions` 安装文档你可以点击这个[链接](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md) 进入查看，比如使用 Git 安装步骤如下：

使用 Git 把项目从仓库 Clone 下来：

```Bash
git clone https://github.com/zsh-users/zsh-autosuggestions ~/.zsh/plugins/zsh-autosuggestions

echo "source ${ZDOTDIR:-$HOME}/.zsh/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc
```


或者手动将以下内容添加到 `.zshrc` 文件内：

```Bash
source ~/.zsh/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh
```


生效：

```Bash
source ~/.zshrc
```


重新开启终端会话，你就可以享受 `zsh-autosuggestions` 给你带来的便利了。

#### 一步安装：

```Bash
git clone https://github.com/zsh-users/zsh-autosuggestions ~/.zsh/plugins/zsh-autosuggestions
echo "source ${ZDOTDIR:-$HOME}/.zsh/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc
source ~/.zshrc

//gitee
git clone git@gitee.com:lhaisu/zsh-autosuggestions.git ~/.zsh/plugins/zsh-autosuggestions
echo "source ${ZDOTDIR:-$HOME}/.zsh/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc
source ~/.zshrc
```


### 方法二：推荐

1. 把插件仓库克隆到`$ZSH_CUSTOM/plugins` (默认位置是 ~/.oh-my-zsh/custom/plugins)

```Bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

```

<img src="https://dev.azure.com/conansteve/87be1d78-05d4-41bd-87b2-a023d463dcd2/_apis/git/repositories/075c6005-9f0d-4b8c-97a7-60d87486d3f4/items?path=%2F1648455923125_2748.png&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0" style="zoom:50%;" />

1. 设置`~/.zshrc`，把`zsh-autosuggestions`添加到 Oh My Zsh 要加载的插件列表中

```Bash
plugins=(git zsh-autosuggestions)
```


1. 使配置生效
	```Bash
	source ~/.zshrc
	```
	

## 语法高亮插件

安装zsh-syntax-highlighting语法高亮插件

官网：[https://github.com/zsh-users/zsh-syntax-highlighting](https://link.jianshu.com/?t=https://github.com/zsh-users/zsh-syntax-highlighting)

### 一步安装：

```Bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.zsh/plugins/zsh-syntax-highlighting
echo "source ${ZDOTDIR:-$HOME}/.zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc
source ~/.zshrc
//gitee
git clone git@gitee.com:jklash1996/zsh-syntax-highlighting.git ~/.zsh/plugins/zsh-syntax-highlighting
echo "source ${ZDOTDIR:-$HOME}/.zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc
source ~/.zshrc
```


## 自动跳转插件autojump

地址：[https://github.com/wting/autojump](https://github.com/wting/autojump)

它的用法是输入 `j 目录名` 或 `j 目录名包含的字符`（这个目录必须是之前 cd 访问过的），就可直接切换到相应的目录。不用再各种`cd`啦～具体看下面截图示例。

![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011530512.png)

#### 方法一：推荐

1. ##### Mac安装

```Bash
brew install autojump
```
> Add the following line to your ~/.bash_profile or ~/.zshrc file:
> ` [ -f /opt/homebrew/etc/profile.d/autojump.sh ] && . /opt/homebrew/etc/profile.d/autojump.sh`
> If you use the Fish shell then add the following line to your ~/.config/fish/config.fish:
> ` [ -f /opt/homebrew/share/autojump/autojump.fish ]; and source /opt/homebrew/share/autojump/autojump.fish`
> Restart your terminal for the settings to take effect.


1. ##### Linux 一步安装

首先下载 autojump 源码

```Bash
git clone git@github.com:wting/autojump.git ~/.zsh/plugins/autojump
cd ~/.zsh/plugins/autojump
./install.py

echo "[[ -s ~/.autojump/etc/profile.d/autojump.sh ]] && source ~/.autojump/etc/profile.d/autojump.sh" >> ${ZDOTDIR:-$HOME}/.zshrc

source ~/.zshrc
```


国内源

```Bash
git clone git@gitee.com:gentlecp/autojump.git ~/.zsh/plugins/autojump

cd ~/.zsh/plugins/autojump

./install.py

echo "[[ -s ~/.autojump/etc/profile.d/autojump.sh ]] && source ~/.autojump/etc/profile.d/autojump.sh" >> ${ZDOTDIR:-$HOME}/.zshrc

source ~/.zshrc
```


安装完成后，使用查看autojump版本。

```Ruby
$ autojump --version
autojump release-v21.1.2
```


## colorls

官网：[https://github.com/athityakumar/colorls](https://github.com/athityakumar/colorls)

### homebrew安装：

```Bash
brew install ruby
sudo gem install colorls
```

> 如果显示`zsh: command not found: colorls`
> 在`.zshrc`里面添加`export PATH=$PATH:$(ruby -e 'puts Gem.bindir')`


### WSL apt安装

```Bash
sudo apt install ruby-dev  //切记用官方源，阿里云源会出问题，会出错，其他源暂时没试过
sudo gem install colorls
```


### MacOS 13.6源码安装：

安装ruby(version>2.5)  [https://www.ruby-lang.org/en/downloads/](https://www.ruby-lang.org/en/downloads/)

[源码安装ruby](https://blog.csdn.net/baidu_38432732/article/details/106573806)

[https://blog.csdn.net/baidu_38432732/article/details/106573806](https://blog.csdn.net/baidu_38432732/article/details/106573806)

```Bash
./configure --prefix=/usr/local/ruby-3.0.3
sudo make
sudo make install
esource ~/.zshrc
ruby -v
gem install colorls
```


如果安装colorls失败，需要安装openssl，命令为`brew install openssl@1.1`

```JavaScript
./config --prefix=/usr/local/opt/openssl/
sudo make
sudo make install
cd  ~/Desktop/ruby-2.7.5/  

//下面功能都是生成makefile
./configure --prefix=/usr/local/opt/ruby-2.7.5 --with-openssl-dir=/usr/local/opt/openssl
./configure --prefix=/usr/local/opt/ruby-2.7.5 --with-openssl-include=/usr/local/opt/openssl/include/ --with-openssl-lib=/usr/local/opt/openssl/lib
//测试成功
cd ./ext/openssl/
ruby extconf.rb --prefix=/usr/local/opt/ruby-2.7.5 --with-openssl-include=/usr/local/opt/openssl/include/ --with-openssl-lib=/usr/local/opt/openssl/lib
//end
 sudo make 
 sudo make install
```


将下面代码添加进.zshrc文件中

```Bash
export RUBY_HOME=/usr/local/opt/ruby-2.7.5
export PATH=$RUBY_HOME/bin:$PATH
export LDFLAGS=“RUBY_HOME/lib”
export CPPFLAGS=“RUBY_HOME/include”
```


### 别名配置文件

```Bash
# colorls别名start
# --sd 排序 
# --gs git状态 Shows git status for each entry
# -r(or)  --report 显示报告
# -d (or) --dirs : Shows only directories
# -f (or) --files : Shows only files
# -h (or) --help : Prints a very helpful help menu
# --sd (or) --sort-dirs or --group-directories-first : Shows directories first, followed by files
alias l='colorls --sd --gs'
alias la='colorls -A --sd --sf --gs --group-directories-first'
alias ll='colorls -l --gs --group-directories-first'
alias lla='colorls -lA --sd --sf --gs --group-directories-first'
alias lt="colorls --tree=1"
alias lt2="colorls --tree=2"
alias lls="ls -lAF"
# colorls别名end
```

# 其他插件

```shell
plugins=(git history vscode sublime sudo)
```

* vscode
* Sublime
* Sudo  

# Hyper

<img src="https://dev.azure.com/conansteve/87be1d78-05d4-41bd-87b2-a023d463dcd2/_apis/git/repositories/075c6005-9f0d-4b8c-97a7-60d87486d3f4/items?path=%2F1648455784134_8713.png&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0" style="zoom:50%;" />

## 安装方法

1. 通过Macwk网站安装
2. MacOS可通过homebrew安装 `brew install hyper`
3. [官网下载](https://hyper.is)

## 配置

```Ruby
copyOnSelect: true,//自动复制被选择区域
shell: 'zsh',
fontFamily: 'Hack Nerd Font Mono, "DejaVu Sans Mono", Consolas, "Lucida Console", monospace',//MacOS  https://www.nerdfonts.com/font-downloads
"editor.fontFamily": "Hack Nerd Font Mono,Lucida Console, ' Lucida Console', Lucida Console，",  //windows
```


这里我们会用到两个插件：

- hyper-snazzy：提供终端颜色主题
- hyper-transparent-dynamic：提供终端窗口毛玻璃半透明效果

具体配置代码如下：

```JSON
plugins: ["hyper-snazzy", "hyper-transparent-dynamic", "hyperpower","hyper-pane"]
```


### 窗口透明度调整

同样是在 Hyper 的配置文件中，添加如下代码：

```JSON
hyperTransparentDynamic: {
    alpha: 0.5 // 默认 50% 透明度
},//节点config的子节点
```


## 主题

```text
hyper i hyper-npm-theme
```


![image (1642×986) (hyper.is)](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011530513.png)

# iterm2

[Mac终端工具iTerm2的多个ssh链接保存设置（类似Xshell的使用方法）](https://blog.csdn.net/ClownG/article/details/107849908)

# 别名配置

## [colorls](#colorls)

## 通用必备配置

```Bash
#git 别名
alias gta="git add ."
alias gtam="git add .  && git commit -m"
alias gtb="git branch"
alias gtbd="git branch -d"
alias gtck="git checkout"
alias gtcl="git clone"
alias gtm="git commit -m"
alias gtl="git log --graph --all"
alias gtlo="git log --oneline --graph --all"
# cancel last add
alias gtr="git reset HEAD"
# cancel last commit and add,慎用，会删除本地文件的修改
alias gtrh="git reset --hard HEAD^"
# cancel last commit
alias gtrs="git reset --soft HEAD^"
# 取消提交，可以先gtrs，再gtr
alias gtps="git push"
alias gts="git status"
alias gtst="git stash"

# convert web page to markdown
alias cm="clean-mark"

alias src="source ~/.zshrc"
alias strc="subl ~/.zshrc"
alias als="alias"
alias alsg="alias |grep"

# convert jupyter notebook to markdown 
alias nb2md="jupyter nbconvert --to markdown" 

# conda alias
alias cda="conda activate"
alias cdd="conda deactivate"
alias cdel="conda env list"

# hexo theme
alias hxcg="hexo clean && hexo g"
alias hxcgs="hexo clean && hexo g && hexo server"
alias hxs="hexo server"
alias hxd="hexo deploy"
```

## 其他配置
```shell
# 普通别名，无法配置colorls时使用
alias l='ls -CF'
alias la='ls -AF '
alias lsa='ls -AF '
alias ll='ls -lF '
alias lla='ls -lAF '

```

# windows terminal

# Reference

1. [终极 Shell——ZSH](https://zhuanlan.zhihu.com/p/19556676)
2. [玩转终端软件 Hyper](https://www.dazhuanlan.com/franco109/topics/1314003)
3. [打造高颜值终端——Hyper](https://sspai.com/post/56081#!)
4. [zsh 命令自动补全插件 zsh-autosuggestions 安装和配置](https://www.jianshu.com/p/43c1b6e40c69)
5. [Linux 懒人工具 - autojump](https://www.jianshu.com/p/15f0ffaa88d7)
6. [Mac终端窗口配置oh-my-zsh](https://www.cnblogs.com/himonkey/p/11853487.html)
7. [Windows Terminal 美化配置](https://www.jianshu.com/p/a61fea170d1a)
8. [打造最强终端之一：Fish shell简明教程](https://blog.csdn.net/lzhujian/article/details/103330056)


