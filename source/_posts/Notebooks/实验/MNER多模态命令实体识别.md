---
title: MNER 多模态命名实体识别
date: 2022-03-31
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
tags: lab
categories:
---


# 数据集

- [Twitter2015](https://github.com/jefferyYu/UMT)



- [Twitter2017](https://github.com/jefferyYu/UMT)

![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011550385.png)

# Baseline

![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011550928.png)

![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011551385.png)

实验结果:

|                            | twitter2015 | twitter2017 |
| -------------------------- | :---------- | ----------- |
| BasicModel                 | 72.614      | 84.002      |
| MMNerModel（bert+crf+ViT） | 72.820      | 84.303      |
| UMT                        | 73.41       | 84.42       |
| HMT-12                     | 73.09       | 84.25       |
| HMT-last                   | 73.20       | 84.25       |
| MYUMT                      | 73.83       | 86.18       |



| alpha | beta | twitter2017 |
| ----- | ---- | ----------- |
| 0.8   | 0.5  | 83.96       |
| 0.8   | 0.8  | 84.19       |
| 1     | 1    | 84.24       |



# 参考资料

[BIOS标注](https://zhuanlan.zhihu.com/p/147537898)

[多模态NER相关论文](https://zhuanlan.zhihu.com/p/161385278)

[多模态深度学习综述：网络结构设计和模态融合方法汇总](https://blog.csdn.net/tMb8Z9Vdm66wH68VX1/article/details/112386111)

[实体关系的联合抽取总结](https://zhuanlan.zhihu.com/p/74886839)
https://zhuanlan.zhihu.com/p/366767181

# 2020

## Improving Multimodal Named Entity Recognition via Entity Span Detection with Unified Multimodal Transformer 

[引用](https://blog.csdn.net/qq_43703681/article/details/113748435)

### 现有方法问题

1. 没有考虑一词多义的上下文表示。
2. 虽然当前方法基于多模态建模获得基于文本的视觉表示，但是在最后隐藏层依然还是只基于文本的表示来进行预测，没有将视觉信息融合进去。
3. 视觉偏差：通常图片只涉及文本中的某一个两个实体，并不涉及其他实体，如果一味的将视觉信息融合进所有实体的识别当中，会导致相关实体识别准确率很高，但是其他实体识别率降低。

### 模型

首先通过Bert和ResNet分别得到文本和图片的上下文向量和视觉特征，之后通过MMI（Transformer的跨模态版本）产生关于文本的视觉表征和关于图片的文本表征。最后通过辅助边界检测任务消除视觉偏差问题。

#### 贡献

- 对于MNER任务首次提出了多模态的Transformer。
- 基于多模态Transformer，设计了一个MNER联合框架，为消除视觉偏差而引入了实体跨度检测辅助任务。


![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011554711.png)

### 实验结果

![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011551385.png)



# 2021

## **Multi-modal Graph Fusion for Named Entity Recognition with Targeted Visual Guidance**

[引用](https://zhuanlan.zhihu.com/p/349064943)

### 模型

![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011555072.png)

## [AAAI 2021 | RpBERT：引入关系传播机制，多模态命名实体识别任务表现优异](https://zhuanlan.zhihu.com/p/478180951)

### 评价

只是建模用了图，实际没有用GNN来来训练

# Think





| 能否引入外部知识库，比如Freebase Dictionary，来解决关联图像噪声 | ![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011555917.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 对于无图像的推文不输入默认图像，而是0向量，借鉴short cut思想，直接在融合模块不进行模态间融合，在预测层，直接将默认第一层输入，使预测结果尽量贴合BERT-CRF模型 | ![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011556670.png) |

- 如何降低抽象图像或者卡通图像等图像噪声？
- 加个单独的分类器判断图像是否是卡通图和表情包，如果是，就降低图像的对文本的权重。
- 适当增加图像相关联的词语获得的注意力权重。
- 兼容BERT-CRF的UMT





![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011556187.png)

# 参考文献

1. A Survey on Deep Learning for Named Entity Recognition