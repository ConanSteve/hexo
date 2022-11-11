---
title: 归一化与正则化
date: 2022-09-09
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
categories:
---
##  Normalization

[特征工程中的「归一化」有什么作用？](https://www.zhihu.com/question/20455227/answer/370658612)

[标准化和归一化，请勿混为一谈，透彻理解数据变换](https://blog.csdn.net/weixin_36604953/article/details/102652160)

[什么是批标准化 (Batch Normalization)](https://zhuanlan.zhihu.com/p/24810318)

[标准化和归一化什么区别？](https://www.zhihu.com/question/20467170)

> 1. 缩放到均值为0，方差为1（**Standardization——**StandardScaler()）
> 2. 缩放到0和1之间（**Standardization——**MinMaxScaler()）
> 3. 缩放到-1和1之间（**Standardization——**MaxAbsScaler()）
> 4. 缩放到0和1之间，保留原始数据的分布（**Normalization——**Normalizer()

[BatchNormalization、LayerNormalization、InstanceNorm、GroupNorm、SwitchableNorm总结](https://blog.csdn.net/liuxiao214/article/details/81037416)
# Reference
1. https://www.jianshu.com/p/0486e225c185