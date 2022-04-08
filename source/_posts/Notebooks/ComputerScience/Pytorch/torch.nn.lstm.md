---
title: torch.nn.LSTM()详解
date: 2022-02-01 10:00:00
author: 陌上人如玉
---

### 输入的参数列表包括:

- `input_size` 输入数据的特征维数，通常就是`embedding_dim`(词向量的维度)
- `hidden_size` LSTM中隐层的维度，`bidirectional` =True时，`hidden_size` 减半
- `num_layers` 循环神经网络的层数
- `bias` 用不用偏置，default=True
- `batch_first` 这个要注意，通常我们输入的数据shape=(`batch_size`, `seq_length`, `embedding_dim`),而`batch_first`默认是False,所以我们的输入数据最好送进LSTM之前将`batch_size`与`seq_length`这两个维度调换
- `dropout` 默认是0，代表不用dropout
- `bidirectional`默认是false，代表不用双向LSTM

### 输入数据包括input,(h_0,c_0):

- `input`就是shape=(`seq_length`, `batch_size`, `input_size`)的张量
- `h_0`是shape=(`num_layers`*`num_directions`, `batch_size`, `hidden_size`)的张量，它包含了在当前这个batch_size中每个句子的初始隐藏状态。其中num_layers就是LSTM的层数。如果`bidirectional`=True, num_directions=2,否则就是１，表示只有一个方向。如果`bidirectional`=True，`hidden_size` //2
- `c_0`和`h_0`的形状相同，它包含的是在当前这个batch_size中的每个句子的初始细胞状态。`h_0`,`c_0`如果不提供，那么默认是０。

### 输出数据包括output,(h_n, c_n):

- `output`的shape=(`seq_length`, `batch_size`, `num_directions`*`hidden_size`),
它包含的是LSTM的最后一时间步的输出特征(h_t),ｔ是batch_size中每个句子的长度。
- `h_n.shape`==(num_directions * num_layers, batch, hidden_size)
- `c_n.shape`==`h_n.shape`
- h_n包含的是句子的最后一个单词（也就是最后一个时间步）的隐藏状态，c_n包含的是句子的最后一个单词的细胞状态，所以 **它们都与句子的长度seq_length无关**。
- `output[-1]`与`h_n`是相等的，(**只有当`bidirectional`=False时才相等，否则`output[-1]`是`h_n`拼接起来的)**，因为`output[-1]`包含的正是`batch_size`个句子中每一个句子的最后一个单词的隐藏状态，注意LSTM中的隐藏状态其实就是输出，cell state细胞状态才是LSTM中一直隐藏的，记录着信息

```python
import torch
batch_size=3
hidden_size=5
embedding_dim=6
seq_length=4
num_layers=1
num_directions=1
vocab_size=20
import numpy as np
input_data=np.random.uniform(0,19,size=(batch_size,seq_length))
input_data=torch.from_numpy(input_data).long()
embedding_layer=torch.nn.Embedding(vocab_size,embedding_dim)
lstm_layer=torch.nn.LSTM(input_size=embedding_dim,hidden_size=hidden_size,num_layers=num_layers,
                        bias=True,batch_first=False,dropout=0.5,bidirectional=False)
lstm_input=embedding_layer(input_data)
assert lstm_input.shape==(batch_size,seq_length,embedding_dim)
lstm_input.transpose_(1,0)
assert lstm_input.shape==(seq_length,batch_size,embedding_dim)
output,(h_n,c_n)=lstm_layer(lstm_input)
assert output.shape==(seq_length,batch_size,hidden_size)
assert h_n.shape==c_n.shape==(num_layers*num_directions,batch_size,hidden_size)

```

![https://img-blog.csdnimg.cn/20200223114310501.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ1NDc4ODY1,size_16,color_FFFFFF,t_70](https://img-blog.csdnimg.cn/20200223114310501.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ1NDc4ODY1,size_16,color_FFFFFF,t_70)

![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011539699.png)

# 参考资料

1. [torch.nn.LSTM()详解](https://blog.csdn.net/m0_45478865/article/details/104455978)