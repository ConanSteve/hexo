---
title: 深度学习理论
date: 2022-01-01 10:00:00
author: 陌上人如玉
mathjax:
katex: true
tags: MachineLearning
categories: 
    机器学习笔记  
---

# 基础

[计算机视觉基本任务综述](https://zhuanlan.zhihu.com/p/262697114)

![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011542238.png)

![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011542239.png)

 卷积层输出尺寸计算公式
$$
\color{OrangeRed}output\_size = \cfrac{input\_size+2\times padding- kernel\_size}{stride}+1
$$


N是输入图片长度，K是滤波器长度（卷积核大小），S是步长

 

## 干货集锦

[机器学习原理](https://www.cntofu.com/book/85/index.html)

[李宏毅机器学习笔记](https://datawhalechina.github.io/leeml-notes/#/)

[李宏毅Bilibili](https://www.bilibili.com/video/av59538266)

[白板推导](https://blog.csdn.net/qq_41485273/article/details/111563979)

 

## 信息论

![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011542240.png)

> I(X;Y) = I(Y;X) = H(Y)-H(Y/X) = H(X) – H(X/Y) 
> H(X) + H(Y) = H(X,Y) + I(X;Y)
> I(X;Y)=H(X) + H(Y) – H(X,Y)

## 基础概念

[详解残差网络](https://zhuanlan.zhihu.com/p/42706477)

[Singular Value Decomposition（SVD奇异值分解）](https://zhuanlan.zhihu.com/p/68386882)

[数据挖掘|概率图模型（一）](https://zhuanlan.zhihu.com/p/22751416)

### 评估标准

[查准率，准确率，查全率](https://www.zhihu.com/question/19645541)

[F1值](https://zhuanlan.zhihu.com/p/97870600)

> 实际上非常简单，**精确率**是针对我们**预测结果**而言的，它表示的是预测为正的样本中有多少是真正的正样本。那么预测为正就有两种可能了，一种就是把[正类](https://www.zhihu.com/search?q=正类&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A91694636})预测为正类(TP)，另一种就是把负类预测为正类(FP)，也就是
> ![](https://www.zhihu.com/equation?tex=P++%3D+%5Cfrac%7BTP%7D%7BTP%2BFP%7D)
> 而**召回率**是针对我们原来的**样本**而言的，它表示的是样本中的正例有多少被预测正确了。那也有两种可能，一种是把原来的正类预测成正类(TP)，另一种就是把原来的正类预测为负类(FN)。
> ![](https://www.zhihu.com/equation?tex=R+%3D+%5Cfrac%7BTP%7D%7BTP%2BFN%7D)

[自监督学习](https://zhuanlan.zhihu.com/p/66063089)

 [超详细的NLP预训练语言模型总结清单](https://mp.weixin.qq.com/s/b2q3nexPR7Amx5ficdBh-Q)

[TF-IDF算法介绍及实现](https://blog.csdn.net/asialee_bird/article/details/81486700)

[马尔可夫毯（Markov Blanket）](https://www.zhihu.com/question/20446337)

[端到端学习](https://www.cnblogs.com/wisir/p/12556353.html)

[特征工程与表示学习](https://zhuanlan.zhihu.com/p/41521695)

[图嵌入](https://zhuanlan.zhihu.com/p/62629465)

[图神经网络](https://zhuanlan.zhihu.com/p/75307407?from_voters_page=true)

[多模态特征表示和融合](https://blog.csdn.net/weixin_48629412/article/details/111174968)



[上采样和下采样](https://blog.csdn.net/tingzhiyi/article/details/114368433)



# 经典算法

## 机器学习算法

[机器学习十大算法系列](https://blog.csdn.net/v_july_v/category_9261611.html)

### 感知机

[感知机](https://www.zhihu.com/question/320426826)

### logistic回归

[logistic回归](https://www.cnblogs.com/geo-will/p/10468356.html)

### EM

> [EM算法](https://blog.csdn.net/u010834867/article/details/90762296)
> [如何通俗理解EM算法](https://blog.csdn.net/v_july_v/article/details/81708386)
> [从EM到Variational EM](https://zhuanlan.zhihu.com/p/32925505)
> [LDA-隐狄利克雷分布-主题模型](https://blog.csdn.net/u012771351/article/details/53032365)

### 贝叶斯

[机器学习|算法笔记-朴素贝叶斯（Naive Bayesian）](https://www.cnblogs.com/geo-will/p/10468401.html)

[从贝叶斯谈到贝叶斯网络](https://blog.csdn.net/v_july_v/article/details/40984699)

[朴素贝叶斯 VS 逻辑回归 区别](https://blog.csdn.net/cjneo/article/details/45167223)

### 支持向量机（SVM）

[推导 | SVM详解（1）SVM基本型](https://zhuanlan.zhihu.com/p/35755150)

[算法笔记-支持向量机](https://www.cnblogs.com/geo-will/p/10503218.html)

### HMM

> **[HMM隐马尔科夫模型](https://zhuanlan.zhihu.com/p/29938926)** 
> **[HMM](https://www.cnblogs.com/pinard/p/6945257.html)**
> **[HMM2](https://blog.csdn.net/weixin_42175217/article/details/105442777?utm_medium=distribute.pc_relevant.none-task-blog-baidujs_baidulandingword-0&spm=1001.2101.3001.4242)**
> **[隐马尔科夫模型](https://blog.csdn.net/hudashi/article/details/87867916)**

**隐马尔可夫模型是 先生成状态序列，然后由状态序列生成观测序列，即是先 P(Z) , 再 P(O|Z), 所以拟合的是 P(O, Z)也就是联合概率分布而判别模型拟合的是条件概率分布。HMM在数据量较少的时候，会脑补数据，性能更好。**



![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011542241.png)

> 条件随机场是一种判别式无向图模型，生成式模型是直接对联合分布进行建模，而判别式模型则是对条件分布进行建模，隐马尔科夫模型（HMM）和马尔科夫随机场都是生成模型，而条件随机场(CRF)是判别式模型。CRF可看作给定观测值的马尔科夫随机场。

维特比算法

[Viterbi维特比算法](https://ah0aangfha.feishu.cn/docs/doccnoVrVCsrIzCEWkxvUlW30hN)

### CRF

[CRF-条件随机场](https://ah0aangfha.feishu.cn/docs/doccnkchwwM1mp9wrcy9NybCgyg)

为了建一个条件随机场，我们首先要定义一个特征函数集，每个特征函数都以整个句子s，当前位置i，位置i和i-1的标签为输入。然后为每一个特征函数赋予一个权重，然后针对每一个标注序列l，对所有的特征函数加权求和，必要的话，可以把求和的值转化为一个概率值。

[CRF-条件随机场](https://www.jianshu.com/p/da49f9a5468c)

[一文理解条件随机场CRF](https://zhuanlan.zhihu.com/p/70067113)

[机器学习 -- 条件随机场 (CRF)](https://zhuanlan.zhihu.com/p/383307632)

[马尔可夫随机场以及条件随机场](https://zhuanlan.zhihu.com/p/112980214)

[最通俗易懂的BiLSTM-CRF模型中的CRF层讲](https://www.sohu.com/a/341284906_787107)

[从隐马尔科夫到条件随机场](https://anxiang1836.github.io/2019/11/05/NLP_From_HMM_to_CRF/)

### 决策树

[决策树(Decision Tree)：通俗易懂之介绍](https://zhuanlan.zhihu.com/p/30059442)

[决策树--信息增益，信息增益比，Geni指数的理解](https://www.cnblogs.com/muzixi/p/6566803.html)



## 其他算法

[随机森林算法及其实现（Random Forest）](https://blog.csdn.net/yangyin007/article/details/82385967) 



# 神经网络概念详解

## 基础概念

### bottleneck

[bottleneck](https://blog.csdn.net/duan19920101/article/details/104349188)



## RNN


[循环神经网络（RNN）浅析](https://www.jianshu.com/p/87aa03352eb9)

[Seq2Seq模型概述](https://www.jianshu.com/p/b2b95f945a98)

[人人都能看懂的LSTM](https://zhuanlan.zhihu.com/p/32085405)



## Transformer

### Attention

* [MultiHeadAttention实现详解](https://zhuanlan.zhihu.com/p/358206572)
* [The Annotated Transformer](http://nlp.seas.harvard.edu/2018/04/03/attention.html)

[attention机制原理及简单实现](https://www.jianshu.com/p/1d67638139da)

[深入理解shortcut](https://blog.csdn.net/baidu_29571167/article/details/89012223)

[Encoder-Decoder](https://blog.csdn.net/qq_38906523/article/details/79838000)

### BERT
#### 论文理论
##### 基础


[词向量之BERT](https://zhuanlan.zhihu.com/p/48612853)
[bert的输入输出是什么](https://zhuanlan.zhihu.com/p/248017234)



[深度学习----Transformer模型之图示进阶篇](https://blog.csdn.net/Sakura55/article/details/86679826)

 [李宏毅-Transformer](https://www.bilibili.com/video/BV1J441137V6)

 [60分钟带你掌握NLP BERT理论与实战](https://www.bilibili.com/video/BV1H441187js?p=1)

 [李宏毅-ELMO, BERT, GPT讲解](https://www.bilibili.com/video/BV17441137fa/?spm_id_from=333.788.videocard.11)

[nlp中的Attention注意力机制+Transformer详解](https://zhuanlan.zhihu.com/p/53682800)

[NLP中的RNN、Seq2Seq与attention注意力机制](https://zhuanlan.zhihu.com/p/52119092)

[nlp中的Attention注意力机制+Transformer详解](https://zhuanlan.zhihu.com/p/53682800)
##### 详解
[Bert详解](https://zhuanlan.zhihu.com/p/54356280)
[Transformer模型详解（图解最完整版）](https://zhuanlan.zhihu.com/p/338817680)
[详解Transformer （Attention Is All You Need）](https://zhuanlan.zhihu.com/p/48508221)
[Bert/Transformer模型的参数大小计算](https://blog.csdn.net/weixin_43922901/article/details/102602557)

#### transformer代码讲解
##### 入门
* [手把手教你用Pytorch-Transformers——部分源码解读及相关说明（一） - 那少年和狗 - 博客园 (cnblogs.com)](https://www.cnblogs.com/dogecheng/p/11907036.html)
* [手把手教你用Pytorch-Transformers——实战（二） - 那少年和狗 - 博客园 (cnblogs.com)](https://www.cnblogs.com/dogecheng/p/11911909.html)

[pytorch-pretrained-bert简单使用](https://blog.csdn.net/mch2869253130/article/details/105538245)  老版库
##### 详解
[transformer代码详解（一）——HuggingFace Transformers最新版本源码解读](https://zhuanlan.zhihu.com/p/360988428)

[bert论文源码详解](https://blog.csdn.net/weixin_39422563/article/details/107180849)

[Huggingface-transformers项目源码剖析及Bert命名实体识别实战](https://blog.csdn.net/weixin_36949593/article/details/106515904)
##### 其他
[Transformer: Training and fine-tuning(六)](https://blog.csdn.net/weixin_42167712/article/details/110890965)

[BERT中的激活函数GELU：高斯误差线性单元](https://zhuanlan.zhihu.com/p/349492378)


### VisionTransformer
[Vision Transformer , Vision MLP 超详细解读 (原理分析+代码解读) (目录)](https://zhuanlan.zhihu.com/p/348593638)

[Vision Transformer（ViT）PyTorch代码全解析（附图解）](https://blog.csdn.net/weixin_44966641/article/details/118733341)

[视觉 Transformer 优秀开源工作：timm 库 vision transformer 代码解读](https://zhuanlan.zhihu.com/p/350837279)

[Vision Transformer（ViT）PyTorch代码全解析（附图解）](https://blog.csdn.net/weixin_44966641/article/details/118733341)

[pytorch中model eval和torch no grad()的区别_江前云后的博客-CSDN博客_torch.nograd](https://blog.csdn.net/songyu0120/article/details/103884586)

[论文解释：Vision Transformers和CNN看到的特征是相同的吗？](https://cloud.tencent.com/developer/article/1891357)

# 经典模型

## VGG16

[VGG16详解](https://www.cnblogs.com/lfri/p/10493408.html)

## ResNet

[一文读懂残差网络ResNet](https://zhuanlan.zhihu.com/p/91385516)

[ResNet网络结构分析](https://zhuanlan.zhihu.com/p/79378841)

# 实战任务

## 文本分类

 [文本分类实战](https://www.cnblogs.com/jiangxinyang/p/10207273.html)

## NER

### 数据集

[序列标注](https://www.jianshu.com/p/5a5bcfe5c185)

[序列标注和中文命名实体识别](https://www.jianshu.com/p/c7c3ace12044)

[命名实体识别学习-数据集介绍-conll03](https://www.datafountain.cn/datasets/5684)

[LSTM+CRF序列标注](https://blog.csdn.net/StarLib/article/details/106933974)

## 关系抽取

[简介](https://www.cnblogs.com/sandwichnlp/p/12049829.html)

[实体关系联合抽取总结](https://zhuanlan.zhihu.com/p/74886839)

[结构学习：序列标注](https://blog.csdn.net/dugudaibo/article/details/79120627)

 

# 多模态

[跨模态检索](https://blog.csdn.net/qq_39388410/article/details/105907097)

[多模态融合](https://blog.csdn.net/qq_39388410/article/details/105145074)

# 问答

[生成模型和判别模型的区别](https://www.zhihu.com/question/20446337)

- 生成模型数据量小时更优，判别模型数据量越大越好
- 生成模型要求数据独立同分布，判别模型没有要求



# TEMP



# Others

[自监督、半监督、无监督学习，傻傻分不清楚？最新综述来帮你！](https://blog.csdn.net/moxibingdao/article/details/106667760)

[有监督学习和无监督学习举例_对比自监督学习](https://blog.csdn.net/weixin_39612677/article/details/110394322)

![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011542242.png)

 

 

 

建议路线，ng课程入门，知道有哪些算法，大致怎么做，然后去kaggle打个入门赛，别做特征工程，把会的算法全用上。然后放下比赛，开始读这本书，同时看机器学习基石或其他比较数学化的进阶课程，这一步不需要你敲代码，你要会的是滚瓜烂熟的推导，做到这一步，再去kaggle参加奖金赛，阅读kernel，学习state of the art 模型，学习特征工程，再在学习过程中阅读最新的论文或者经典的论文，不断迭代这个过程，别淹死在什么机器学习实战上，有现成的轮子不用，非得费那个劲，除非你科班毕业，代码能力扎实，不然你能不能从头实现一遍决策树对你找不找到工作没有任何一毛钱关系。笔试不会考你如何实现hmm，只会考数据结构与算法，面试只会让你推导。