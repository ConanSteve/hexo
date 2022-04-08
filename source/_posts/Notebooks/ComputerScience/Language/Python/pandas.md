---
title: pandas常用用法
date: 2022-03-31
author: 陌上人如玉
comments:
description: pandas读取excel，csv文件，并插入删除数据
keywords: pandas
top_img:
cover:
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
tags: python,
categories: Python
---

## 读取文件

### 读取excel文件

```python
import pandas as pd
df = pd.read_excel(file_path, sheet_name)
```

### 读取csv文件

```python
import pandas as pd
df = pd.read_csv(file_path)
```

## 写入文件

创建一个DataFrame对象，设置列名，data可为二维数组

```python
df = pd.DataFrame(data=None, columns = ["disease", "relation", "object"])
```

写入文件

```python
df.to_csv(file_path, index = False, sep=",")
```



## 循环迭代数据

```python
for row in range(df.shape[0]):
  data = df.loc[row, "Month_No"] 
```



## 尾部插入数据

```python
import pandas as pd
s = pd.Series([6,8,3,1,12])
df = pd.DataFrame(s,columns=['Month_No'])
df.insert(1,"No_of_days",[30,31,31,31,31],True)# 插入列
print (df)
```
>									Month_No  No_of_days 
>				0         6          30 
>				1         8          31 
>				2         3          31 
>				3         1          31 
>				4        12          31

```python
df = df.append({"Month_No":7,"No_of_days":31},ignore_index=True)
print(df)
```

>																		Month_No  No_of_days 
>													0         6          30 
>													1         8          31 
>													2         3          31 
>													3         1          31 
>													4        12          31
>													5         7          31

### concat插入

append方法已经废弃，推荐使用concat方法

```python
df_tmp=pd.DataFrame([[7,31]], columns=["Month_No", "No_of_days"])
df = pd.concat([df_tmp, df], ignore_index = True)
```



# Reference

1. [pandas尾部追加行记录append](https://www.cnblogs.com/jm7612/p/12495020.html)