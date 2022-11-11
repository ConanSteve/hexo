---
title: 将jupyter notebook转成Markdown文件
date: 2022-04-08
author: 陌上人如玉
comments:
description:
keywords: jupyter, markdown
top_img:
cover:
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
tags: markdown
categories:
  [编程语言, Python]
---

## 一、准备工作

安装nbconverter: [nbconvert: Convert Notebooks to other formats](https://link.zhihu.com/?target=https%3A//nbconvert.readthedocs.io/en/latest/)

```python
pip install nbconvert
```

**注意依赖项：**

- **基本依赖：pandoc**

```python
pip install pandoc
```

- **如果需要转tex：**[http://tug.org/texlive/](https://link.zhihu.com/?target=http%3A//tug.org/texlive/)
- 如果需要转pdf: Chromium [pyppeteer/pyppeteer](https://link.zhihu.com/?target=https%3A//github.com/pyppeteer/pyppeteer)

![img](https://pic4.zhimg.com/80/v2-ca3061832df5003c5afbcdc20a06bdc3_1440w.jpg)

## 二、使用方法

命令行：

```python
$ jupyter nbconvert --to FORMAT notebook.ipynb
```

这里`FORMAT` 用具体的格式替换，如 `markdown`, `html`等。

例如：

```python
$ jupyter nbconvert --to markdown notebook.ipynb
```

可以将别名添加进zshrc文件

```shell
alias nb2md="jupyter nbconvert --to markdown"
```



## 三、测试

准备一个`ipynb`文件：

![img](https://pic1.zhimg.com/v2-504b4ce2a7050186d851c528b532b1e8_b.jpg)



这里为了测试它的性能，特意画了一个图。

用上述命令转格式，在`Typora`打开：

![img](https://pic4.zhimg.com/v2-51f77e331b6ce419a88b4749c9c83eb3_b.jpg)



对比内容：

![img](https://pic2.zhimg.com/v2-239bc117b705dd6aec187c3990225e79_b.jpg)



一模一样。

## 四、其它问题

- 1、支持的其它类型文件：

![img](https://pic2.zhimg.com/80/v2-1b985561f9fa9412c23ba89f54ffc855_1440w.jpg)

- 2、 可以在命令行实现多个文件导出

![img](https://pic2.zhimg.com/80/v2-984c7cc19f54f7082d969529a2521d75_1440w.jpg)

只需要写一个`py`文件即可，如上图第二个cell。

- 3、`nbconverter`还可以直接作为 `python`库来使用

详见官网：[Using nbconvert as a library](https://link.zhihu.com/?target=https%3A//nbconvert.readthedocs.io/en/latest/nbconvert_library.html)

# Reference

1. 转载自[Jupyter Notebook文件转markdown](https://zhuanlan.zhihu.com/p/371132826)