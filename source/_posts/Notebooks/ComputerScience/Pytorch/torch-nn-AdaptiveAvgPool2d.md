---
title: torch.nn.AdaptiveAvgPool2d() 自适应平均池化函数解析
date: 2022-04-18
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
categories: Pytorch

---

先来看一段代码：

AdaptiveAvgPool2d在参数中只指定了输出的大小（1，1）。

```python
net = nn.Sequential(b1, b2, b3, b4, b5,
                    nn.AdaptiveAvgPool2d((1,1)),
                    nn.Flatten(), nn.Linear(512, 10))
```

nn.AdaptiveAvgPool2d((1,1))，首先这句话的含义是使得池化后的每个通道上的大小是一个1x1的，也就是每个通道上只有一个像素点。（1，1）表示的outputsize。

原型如下：

如题：只需要给定输出特征图的大小就好，其中通道数前后不发生变化。具体如下：

**AdaptiveAvgPool2d**

CLASStorch.nn.AdaptiveAvgPool2d(output_size)[[SOURCE\]](https://link.zhihu.com/?target=https%3A//pytorch.org/docs/master/_modules/torch/nn/modules/pooling.html%23AdaptiveAvgPool2d)

Applies a 2D adaptive average pooling over an input signal composed of several input planes.

The output is of size H x W, for any input size. The number of output features is equal to the number of input planes.

Parameters

**output_size** – the target output size of the image of the form H x W. Can be a tuple (H, W) or a single H for a square image H x H. H and W can be either a int, or None which means the size will be the same as that of the input.



普通的2d池化如下：

在参数中指定了kernel_size,stride and padding。

```python
b1 = nn.Sequential(nn.Conv2d(1, 64, kernel_size=7, stride=2, padding=3),
                   nn.BatchNorm2d(64), nn.ReLU(),
                   nn.MaxPool2d(kernel_size=3, stride=2, padding=1))
```
