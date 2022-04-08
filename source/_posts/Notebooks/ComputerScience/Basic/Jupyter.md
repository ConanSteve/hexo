---
title: jupyter入门
date: 2022-02-01 10:00:00
author: 陌上人如玉
---

### 入门

[Jupyter Notebook介绍、安装及使用教程](https://www.jianshu.com/p/91365f343585)

###  安装

```
conda install jupyter notebook
```

### 进入笔记

```
jupyter notebook
```

### 增删虚拟环境

>  [Jupyter Notebook 增加kernel的方法](https://blog.csdn.net/wj1066/article/details/72891667)
> [Jupyter Notebook导入和删除虚拟环境](https://blog.csdn.net/liuestcjun/article/details/101981269)
> [在Jupyter Notebook中选择特定的虚拟环境](https://blog.csdn.net/liminwang0311/article/details/86565111)

```Shell
conda install -n pytorch ipykernel
conda activate pytorch
python -m ipykernel install --user --name pytorch --display-name pytorch3.7
```

删除 `jupyter kernelspec remove pytorch`

显示列表 `jupyter kernelspec list` 

# Reference

[关于 Jupyter Notebook 中 No module named 'torch' 的解决办法](https://blog.csdn.net/weixin_41923658/article/details/103356336?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param) 