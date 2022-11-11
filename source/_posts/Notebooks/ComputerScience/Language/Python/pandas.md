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
tags: python
categories:
  [编程语言, Python]
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



## 插入整列数据

```python
import pandas as pd
s = pd.Series([6,8,3,1,12])
df = pd.DataFrame(s,columns=['Month_No'])
df.insert(1,"No_of_days",[30,31,31,31,31],True)# 插入列
df
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Month_No</th>
      <th>No_of_days</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6</td>
      <td>30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8</td>
      <td>31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>31</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>31</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12</td>
      <td>31</td>
    </tr>
  </tbody>
</table>

## 尾部插入数据
### append插入
```python
df = df.append({"Month_No":7,"No_of_days":31},ignore_index=True)
df
```
### concat插入

append方法已经废弃，推荐使用concat方法

```python
df_tmp=pd.DataFrame([[7,31],[4,30]], columns=["Month_No", "No_of_days"])
df = pd.concat([df, df_tmp], ignore_index = True)
df
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Month_No</th>
      <th>No_of_days</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6</td>
      <td>30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8</td>
      <td>31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>31</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>31</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12</td>
      <td>31</td>
    </tr>
    <tr>
      <th>5</th>
      <td>7</td>
      <td>31</td>
    </tr>
    <tr>
      <th>6</th>
      <td>4</td>
      <td>30</td>
    </tr>
  </tbody>
</table>

## 修改列名
### 暴力修改


```python
df.columns=['MonthNo','NoOfDays']  
df
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>MonthNo</th>
      <th>NoOfDays</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6</td>
      <td>30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8</td>
      <td>31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>31</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>31</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12</td>
      <td>31</td>
    </tr>
  </tbody>
</table>


### 利用rename修改 

注意：`inplace`参数不能省略


```python
df.rename(columns={'MonthNo':'Month_No','NoOfDays':'No_of_days'},inplace=True) 
df
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Month_No</th>
      <th>No_of_days</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6</td>
      <td>30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8</td>
      <td>31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>31</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>31</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12</td>
      <td>31</td>
    </tr>
  </tbody>
</table>

## 删除列数据
* [参考](https://www.cnblogs.com/wodexk/p/10316674.html)

`df.drop()`
axis=1: 删除列
```python
feature_1 = df_feature_all.drop(labels=["structure of ionizable lipid (SMILE)","IgG"],axis=1).to_numpy()
```

# Reference

1. [pandas尾部追加行记录append](https://www.cnblogs.com/jm7612/p/12495020.html)