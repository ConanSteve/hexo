---
title: 训练时的学习率调整：optimizer和scheduler
date: 2022-04-28
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
  [Pytorch]
---

最近在用mmdection框架修改网络的时候发现，网络训练起来一直都不收敛，训练一小会就换全部变nan，检测了好久都没有发现什么问题，最终修改了学习率，终于可以收敛了。但是关于怎么调整学习率一直都还没有掌握。因此特意写了这一篇进行总结。

## **1.optimizer.step()和scheduler.step()的区别**

optimizer.step()和scheduler.step()是我们在训练网络之前都需要设置。我理解的是optimizer是指定**使用哪个优化器**，scheduler是**对优化器的学习率进行调整**，正常情况下训练的步骤越大，学习率应该变得越小。optimizer.step()通常用在每个mini-batch之中，而scheduler.step()通常用在epoch里面,但是不绝对。可以根据具体的需求来做。只有用了optimizer.step()，模型才会更新，而scheduler.step()是对lr进行调整。通常我们在scheduler的step_size表示scheduler.step()每调用step_size次，对应的学习率就会按照策略调整一次。所以如果scheduler.step()是放在mini-batch里面，那么step_size指的是经过这么多次迭代，学习率改变一次。下面为一个简单的使用实例：

```python
optimizer = optim.SGD(model.parameters(), lr = 0.01, momentum = 0.9)
scheduler = lr_scheduler.StepLR(optimizer, step_size = 100, gamma = 0.1)
model = net.train(model, loss_function, optimizer, scheduler, num_epochs = 100)
```



## 2.1optimizer的种类

### 2.1 optim.SGD

### 2.2 optim.Adam



## **3.**  scheduler **的种类**

pytorch有torch.optim.lr_scheduler模块提供了一些根据epoch训练次数来调整学习率（learning rate）的方法。一般情况下我们会设置随着epoch的增大而逐渐减小学习率从而达到更好的训练效果。学习率的调整应该放在optimizer更新之后，下面是一个参考伪代码：

```text
scheduler = ...

for epoch in range(100):
     train(...)
     validate(...)
     scheduler.step()
```

本文介绍的调整学习率的函数都是基于epoch大小变化进行调整的。



### 3.1torch.optim.lr_scheduler.LambdaLR

> class torch.optim.lr_scheduler.LambdaLR(optimizer, lr_lambda, last_epoch=-1)

学习率的更新公式为： ![](https://www.zhihu.com/equation?tex=%5Ctext+%7B+new_l+%7D+r%3D%5Clambda+%5Ctimes+%5Ctext+%7B+initial_l+%7D+r)

![](https://www.zhihu.com/equation?tex=%5Ctext+%7B+new_l+%7D+r) 是得到的新的学习率， ![](https://www.zhihu.com/equation?tex=%5Ctext+%7B+initial_l+%7D+r) 是初始的学习率，λ是通过参数lr_lambda和epoch得到的。

* optimizer （Optimizer）：要更改学习率的优化器；
* lr_lambda（function or list）：根据epoch计算λ的函数；或者是一个list的这样的function，分别计算各个parameter groups的学习率更新用到的λ；
* last_epoch （int）：最后一个epoch的index，如果是训练了很多个epoch后中断了，继续训练，这个值就等于加载的模型的epoch。默认为-1表示从头开始训练，即从epoch=1开始。

```python
import torch
import torch.nn as nn
from torch.optim.lr_scheduler import LambdaLR

initial_lr = 0.1
net_1 = model()

optimizer_1 = torch.optim.Adam(net_1.parameters(), lr = initial_lr)
scheduler_1 = LambdaLR(optimizer_1, lr_lambda=lambda epoch: 1/(epoch+1))

print("初始化的学习率：", optimizer_1.defaults['lr'])

for epoch in range(1, 11):
    # train
    optimizer_1.zero_grad()
    optimizer_1.step()
    print("第%d个epoch的学习率：%f" % (epoch, optimizer_1.param_groups[0]['lr']))
    scheduler_1.step()
```
```text
初始化的学习率： 0.1
第1个epoch的学习率：0.100000
第2个epoch的学习率：0.050000
第3个epoch的学习率：0.033333
第4个epoch的学习率：0.025000
第5个epoch的学习率：0.020000
第6个epoch的学习率：0.016667
第7个epoch的学习率：0.014286
第8个epoch的学习率：0.012500
第9个epoch的学习率：0.011111
第10个epoch的学习率：0.010000
```



### 3.2 torch.optim.lr_scheduler.StepLR

```text
class torch.optim.lr_scheduler.StepLR(optimizer, step_size, gamma=0.1, last_epoch=-1)
```

学习率的更新公式为： ![](https://www.zhihu.com/equation?tex=%5Ctext+%7B+new_l+%7D+r%3D%5Ctext+%7B+initial_l+%7D+r+%5Ctimes+%5Cgamma%5E%7B%5Ctext+%7Bepoch+%7D+%2F+%2F+%5Ctext+%7B+step_size+%7D%7D)

参数：

* optimizer （Optimizer）：要更改学习率的优化器；
* step_size（int）：每训练step_size个epoch，更新一次参数；
* gamma（float）：更新lr的乘法因子；
* last_epoch （int）：最后一个epoch的index，如果是训练了很多个epoch后中断了，继续训练，这个值就等于加载的模型的epoch。默认为-1表示从头开始训练，即从epoch=1开始。

```python
import torch
import torch.nn as nn
from torch.optim.lr_scheduler import StepLR

initial_lr = 0.1
net_1 = model()

optimizer_1 = torch.optim.Adam(net_1.parameters(), lr = initial_lr)
scheduler_1 = StepLR(optimizer_1, step_size=3, gamma=0.1)

print("初始化的学习率：", optimizer_1.defaults['lr'])

for epoch in range(1, 11):
    # train
    optimizer_1.zero_grad()
    optimizer_1.step()
    print("第%d个epoch的学习率：%f" % (epoch, optimizer_1.param_groups[0]['lr']))
    scheduler_1.step()
```
```text
初始化的学习率： 0.1
第1个epoch的学习率：0.100000
第2个epoch的学习率：0.100000
第3个epoch的学习率：0.100000
第4个epoch的学习率：0.010000
第5个epoch的学习率：0.010000
第6个epoch的学习率：0.010000
第7个epoch的学习率：0.001000
第8个epoch的学习率：0.001000
第9个epoch的学习率：0.001000
第10个epoch的学习率：0.000100
```



### 3.3 torch.optim.lr_scheduler.MultiStepLR

```text
class torch.optim.lr_scheduler.MultiStepLR(optimizer, milestones, gamma=0.1, last_epoch=-1)
```

学习率的更新公式为： ![](https://www.zhihu.com/equation?tex=n+e+w_%7B-l%7D+r%3D%5Ctext+%7B+initial_lr+%7D+%5Ctimes+%5Cgamma%5E%7B%5Ctext+%7Bbisect_right+%7D%28%5Ctext+%7B+milestones%2Cepoch+%7D%29%7D)

参数：

* optimizer （Optimizer）：要更改学习率的优化器；
* milestones（list）：递增的list，存放要更新lr的epoch；
* gamma（float）：更新lr的乘法因子；
* last_epoch （int）：最后一个epoch的index，如果是训练了很多个epoch后中断了，继续训练，这个值就等于加载的模型的epoch。默认为-1表示从头开始训练，即从epoch=1开始。

```python
import torch
import torch.nn as nn
from torch.optim.lr_scheduler import MultiStepLR

initial_lr = 0.1
net_1 = model()

optimizer_1 = torch.optim.Adam(net_1.parameters(), lr = initial_lr)
scheduler_1 = MultiStepLR(optimizer_1, milestones=[3, 7], gamma=0.1)

print("初始化的学习率：", optimizer_1.defaults['lr'])

for epoch in range(1, 11):
    # train
    optimizer_1.zero_grad()
    optimizer_1.step()
    print("第%d个epoch的学习率：%f" % (epoch, optimizer_1.param_groups[0]['lr']))
    scheduler_1.step()
```
```text
初始化的学习率： 0.1
第1个epoch的学习率：0.100000
第2个epoch的学习率：0.100000
第3个epoch的学习率：0.100000
第4个epoch的学习率：0.010000
第5个epoch的学习率：0.010000
第6个epoch的学习率：0.010000
第7个epoch的学习率：0.010000
第8个epoch的学习率：0.001000
第9个epoch的学习率：0.001000
第10个epoch的学习率：0.001000
```



### 3.4 torch.optim.lr_scheduler.ExponentialLR

```text
class torch.optim.lr_scheduler.ExponentialLR(optimizer, gamma, last_epoch=-1)
```

学习率的更新公式为： ![](https://www.zhihu.com/equation?tex=n+e+w_%7B-l%7D+r%3D%5Ctext+%7B+initial_l+%7D+r+%5Ctimes+%5Cgamma%5E%7B%5Ctext+%7Bepoch+%7D%7D)



参数：

* optimizer （Optimizer）：要更改学习率的优化器；
* gamma（float）：更新lr的乘法因子；
* last_epoch （int）：最后一个epoch的index，如果是训练了很多个epoch后中断了，继续训练，这个值就等于加载的模型的epoch。默认为-1表示从头开始训练，即从epoch=1开始。

```python
import torch
import torch.nn as nn
from torch.optim.lr_scheduler import ExponentialLR

initial_lr = 0.1
net_1 = model()

optimizer_1 = torch.optim.Adam(net_1.parameters(), lr = initial_lr)
scheduler_1 = ExponentialLR(optimizer_1, gamma=0.1)

print("初始化的学习率：", optimizer_1.defaults['lr'])

for epoch in range(1, 11):
    # train
    optimizer_1.zero_grad()
    optimizer_1.step()
    print("第%d个epoch的学习率：%f" % (epoch, optimizer_1.param_groups[0]['lr']))
    scheduler_1.step()
```
```text
初始化的学习率： 0.1
第1个epoch的学习率：0.100000
第2个epoch的学习率：0.010000
第3个epoch的学习率：0.001000
第4个epoch的学习率：0.000100
第5个epoch的学习率：0.000010
第6个epoch的学习率：0.000001
第7个epoch的学习率：0.000000
第8个epoch的学习率：0.000000
第9个epoch的学习率：0.000000
第10个epoch的学习率：0.000000
```





# Reference

1. [训练时的学习率调整：optimizer和scheduler](https://zhuanlan.zhihu.com/p/344294796)
2. [optimizer.step()和scheduler.step()_于小勇的博客-CSDN博客](https://link.zhihu.com/?target=https%3A//blog.csdn.net/weixin_36670529/article/details/107144074)
3. [[pytorch] torch.optimizer.lr_scheduler调整学习率](https://link.zhihu.com/?target=https%3A//blog.csdn.net/weixin_43844219/article/details/104319339%3Futm_medium%3Ddistribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-1.control%26depth_1-utm_source%3Ddistribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-1.control)
3. [醒了么：PyTorch--lr_scheduler.step()和optimizer.step()的先后顺序](https://zhuanlan.zhihu.com/p/136902153)
