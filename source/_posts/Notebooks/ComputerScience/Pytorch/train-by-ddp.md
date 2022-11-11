---
title: 多GPU训练
date: 2021-10-10T04:00:19.000Z
---
对pytorch多GPU训练有一定的疑惑，这里做一个记录。
首先要对pytorch中的两种并行训练实现方式：1.DataParallel； 2.DDP有一定的认识。可参考:

Pytorch 中通过 torch.distributed 包提供分布式支持，包括 GPU 和 CPU 的分布式训练支持。Pytorch 分布式目前只支持 Linux。

在此之前，torch.nn.DataParallel 已经提供数据并行的支持，但是其不支持多机分布式训练，且底层实现相较于 distributed 的接口，有些许不足。

torch.distributed 的优势如下：

**每个进程对应一个独立的训练过程**，且只对梯度等少量数据进行信息交换。
在每次迭代中，每个进程具有自己的 **optimizer** ，并独立完成所有的优化步骤，进程内与一般的训练无异。

在各进程梯度计算完成之后，各进程需要将梯度进行汇总平均，然后再由 rank=0 的进程，将其 broadcast 到所有进程。之后，各进程用该梯度来更新参数。

由于 **各进程中的模型，初始参数一致** (初始时刻进行一次 broadcast)，而每次用于更新参数的梯度也一致，因此，各进程的模型参数始终保持一致。

而在 DataParallel 中，全程维护一个 optimizer，对各 GPU 上梯度进行求和，而在主 GPU 进行参数更新，之后再将模型参数 broadcast 到其他 GPU。

相较于 DataParallel，torch.distributed 传输的数据量更少，因此速度更快，效率更高。

distributed的方式会在每个GPU上单独放一个 **模型副本，optimizer副本，不同的dataloader**

## 1. rank

* rank：
表示进程序号，用于进程间通讯，表征进程优先级。rank = 0 的主机为 master 节点。
* local_rank：
进程内， **GPU 编号**， **非显式参数**，由 **torch.distributed.launch** 内部指定。比方说， rank = 3，local_rank = 0 表示第 3 个进程内的第 1 块 GPU。

## 2. init_process_group初始化

分布式训练的时候，有多种初始化方式，参考链接的第二篇文章。比较常用的是nccl的。

```
torch.distributed.init_process_group(backend='nccl', init_method='env://')  # distributed backend
```

## 3. DistributedSampler

**多GPU训练的时候，采用DDP的方式，每个GPU上都有一个模型副本，正确的情况应该是每个GPU上送入不同的数据，前向，求loss，整合loss，反向梯度**
pytorch中有DistributedSampler实现对单个dataset进行多GPU分发。详情看后面的例子

**应该还要将对应的数据放到不同的GPU上，比如用：input = input.to(device)**

## 4. DistributedDataParallel

模型封装：

* 将模型放到对应的GPU上
* 对模型进行封装

```python
print("模型搬移到GPU：", device)
model.to(device)

if torch.cuda.device_count() > 1:
    print("Let's use", torch.cuda.device_count(), "GPUs!")

    print("模型封装的gpu：", local_rank)
    model = torch.nn.parallel.DistributedDataParallel(model,
                                                      device_ids=[local_rank],
                                                      output_device=local_rank)
```

## 5. 例子

这里用一个简单的例子对以上的几个方面进行测试，单机多卡的情况。
**test.py**

```python
import torch
import torch.nn as nn
from torch.autograd import Variable
from torch.utils.data import Dataset, DataLoader
import os
from torch.utils.data.distributed import DistributedSampler
import argparse

def parse_args():
    parser = argparse.ArgumentParser(description='Train Multitask network')

    parser.add_argument('--sync-bn', action='store_true', help='use SyncBatchNorm, only available in DDP mode')
    parser.add_argument('--local_rank', type=int, default=-1, help='DDP parameter, do not modify')
    parser.add_argument('--conf-thres', type=float, default=0.001, help='object confidence threshold')
    parser.add_argument('--iou-thres', type=float, default=0.6, help='IOU threshold for NMS')
    args = parser.parse_args()

    return args

args = parse_args()
print("local_rank: ", args.local_rank)

torch.distributed.init_process_group(backend='nccl', init_method='env://')

input_size = 5
output_size = 2
batch_size = 4
data_size = 40

local_rank = torch.distributed.get_rank()
print("local rank: ", local_rank)
torch.cuda.set_device(local_rank)
device = torch.device("cuda", local_rank)
print("device: ", device)

class RandomDataset(Dataset):
    def __init__(self, size, length):
        self.len = length
        self.data = torch.randn(length, size).to('cuda')

    def __getitem__(self, index):
        return self.data[index]

    def __len__(self):
        return self.len

dataset = RandomDataset(input_size, data_size)
print("length dataset: " , len(dataset))

sampler = iter(DistributedSampler(dataset))

listsampler = list(sampler)
print("list sampler len:", len(listsampler))
print("list sampler", listsampler)
print("sort sampler: ", sorted(listsampler))

rand_loader = DataLoader(dataset=dataset,
                         batch_size=batch_size,
                         sampler=DistributedSampler(dataset))

class Model(nn.Module):
    def __init__(self, input_size, output_size):
        super(Model, self).__init__()
        self.fc = nn.Linear(input_size, output_size)

    def forward(self, input):
        output = self.fc(input)
        print("  In Model: input size", input.size(),
              "output size", output.size())
        return output

model = Model(input_size, output_size)

print("模型搬移到GPU：", device)
model.to(device)

if torch.cuda.device_count() > 1:
    print("Let's use", torch.cuda.device_count(), "GPUs!")

    print("模型封装的gpu：", local_rank)
    model = torch.nn.parallel.DistributedDataParallel(model,
                                                      device_ids=[local_rank],
                                                      output_device=local_rank)

for data in rand_loader:
    if torch.cuda.is_available():
        input_var = data
    else:
        input_var = data

    output = model(input_var)
    print("Outside: input size", input_var.size(), "output_size", output.size())
```

命令：`CUDA_VISIBLE_DEVICES=0,1 python -m torch.distributed.launch --nproc_per_node=2 test.py`

输出：

```
*****************************************
Setting OMP_NUM_THREADS environment variable for each process to be 1 in default, to avoid your system being overloaded, please further tune the variable for optimal performance in your application as needed. 
*****************************************
local_rank:  1
local_rank:  0
local rank:  0
local rank:  1
device:  device:  cuda:1
cuda:0
length dataset:  40
length dataset:  40
list sampler len: 20
list sampler [16, 5, 14, 29, 26, 6, 25, 1, 32, 18, 0, 19, 36, 7, 38, 30, 12, 34, 22, 13]
sort sampler:  [0, 1, 5, 6, 7, 12, 13, 14, 16, 18, 19, 22, 25, 26, 29, 30, 32, 34, 36, 38]
list sampler len: 20
list sampler [4, 21, 11, 39, 17, 2, 20, 24, 15, 28, 9, 10, 8, 27, 37, 31, 35, 3, 33, 23]
sort sampler:  [2, 3, 4, 8, 9, 10, 11, 15, 17, 20, 21, 23, 24, 27, 28, 31, 33, 35, 37, 39]
模型搬移到GPU：模型搬移到GPU：  cuda:1
cuda:0
Let's use 2 GPUs!
模型封装的gpu：Let's use  12
 GPUs!
模型封装的gpu： 0
  In Model: input size torch.Size([4, 5]) output size torch.Size([4, 2])
Outside: input size torch.Size([4, 5]) output_size torch.Size([4, 2])
  In Model: input size torch.Size([4, 5]) output size torch.Size([4, 2])
Outside: input size torch.Size([4, 5]) output_size torch.Size([4, 2])
  In Model: input size torch.Size([4, 5]) output size torch.Size([4, 2])
Outside: input size torch.Size([4, 5]) output_size torch.Size([4, 2])
  In Model: input size torch.Size([4, 5]) output size torch.Size([4, 2])
Outside: input size torch.Size([4, 5]) output_size torch.Size([4, 2])
  In Model: input size torch.Size([4, 5]) output size torch.Size([4, 2])
Outside: input size torch.Size([4, 5]) output_size torch.Size([4, 2])
  In Model: input size torch.Size([4, 5]) output size torch.Size([4, 2])
Outside: input size torch.Size([4, 5]) output_size torch.Size([4, 2])
  In Model: input size torch.Size([4, 5]) output size torch.Size([4, 2])
Outside: input size torch.Size([4, 5]) output_size torch.Size([4, 2])
  In Model: input size torch.Size([4, 5]) output size torch.Size([4, 2])
Outside: input size torch.Size([4, 5]) output_size torch.Size([4, 2])
  In Model: input size torch.Size([4, 5]) output size torch.Size([4, 2])
Outside: input size torch.Size([4, 5]) output_size torch.Size([4, 2])
  In Model: input size torch.Size([4, 5]) output size torch.Size([4, 2])
Outside: input size torch.Size([4, 5]) output_size torch.Size([4, 2])
```

可以看到：

* local_rank是 `torch.distributed.launch`隐含指定的，这里我们指定了2块GPU，分别启动了2个两个线程，所以 `torch.distributed.launch`会将local_rank设为0，1
* 两个DistributedSampler是len(dataset)的一半，切二者的index数是不重合的
* 模型是单独分配到某个GPU，再进行封装的。

## reference

1. [Origin](https://blog.csdn.net/u011622208/article/details/120682874)
