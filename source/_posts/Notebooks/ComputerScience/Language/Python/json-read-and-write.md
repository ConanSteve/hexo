---
title: python中json文件的读写
date: 2022-03-31
author: 陌上人如玉
comments:
description: python中json文件的读写和格式化输出
keywords:
top_img: 
cover: img/pages/gf/qljst.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
tags: python
categories:
  [编程语言, Python]
---

## 输入json

将json文件读取为dict类型

```python
import json
with open("/data.json", 'r', encoding='utf8') as fp:
  json_data = json.load(fp)
print('这是文件中的json数据：',json_data)
print('这是读取到文件数据的数据类型：', type(json_data))
```



## 输出json

### 输出到文件

```python
import json
dic={'a': 1, 'c': 3, 'b': 2}
with open("/output.json", "w", encoding='utf8') as f:
	json.dump(dic, f, indent=4, ensure_ascii=False)
```



### 输出到终端

```python
print(json.dumps(dic, sort_keys=True, indent=4, separators=(',', ':')))
```




### 参数详解

* sort_keys：是否按照字典排序（a-z）输出，True代表是，False代表否。
* indent=4：设置缩进格数，一般由于Linux的习惯，这里会设置为4。
* separators：设置分隔符，在`dic = {'a': 1, 'b': 2, 'c': 3}`这行代码里可以看到冒号和逗号后面都带了个空格，这也是因为Python的默认格式也是如此，如果不想后面带有空格输出，那就可以设置成`separators=(',', ':')`，如果想保持原样，可以写成`separators=(', ', ': ')`。

