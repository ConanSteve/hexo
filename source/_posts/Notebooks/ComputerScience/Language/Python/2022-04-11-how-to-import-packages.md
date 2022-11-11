---
title: 导入自定义包的三种导入方式
date: 2022-04-11
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
tags: python
categories:
  [编程语言, Python]

---

# 1.自定义包

`包`就是一个至少包含`__init__.py`文件的文件夹，这个文件是**必须存在**的，否则，`Python`就把这个目录当成**普通目录(文件夹)**，而不是一个`包`。`__init__.py`可以是**空文件**，也可以有`Python代码`，因为`__init__.py`**本身就是一个模块**，而它的模块名就是对应包的名字。**调用包就是执行包下的**`__init__.py`**文件**。

以下自定义了一个包，包所在的目录为`D:\Code_Sources\Python\Test\`，即就是这个目录下有个叫`parent`的包。

![img](https://ask.qcloudimg.com/http-save/yehe-7042105/wnivgqa3zo.png?imageView2/2/w/1620)

## 1.1. parent 目录中的文件

### **init**.py

```python
# parent 的 __init__.py

if __name__ == '__main__':
    print('parent 作为主程序运行')
else:
    print('parent 初始化')
```

## 1.2. pack 目录中的文件

### **init**.py

```python
# Pack 的 __init__.py

if __name__ == '__main__':
    print('作为主程序运行')
else:
    print('Pack初始化')
```

### [mod.py](http://mod.py/)

```python
# mod
def func():
    print('pack.mod.func()')

if __name__ == '__main__':
    print('mod 作为主程序运行')
else:
    print('mod 被另一个模块调用')
```

## 1.3. pack2 目录中的文件

### **init**.py

```python
# Pack2 的 __init__.py

# __all__ 用于当前Pack2包是所包含的模块
__all__ = ["mod2_1", "mod2_2", "mod2_3"]

if __name__ == '__main__':
    print('Pack2作为主程序运行')
else:
    print('Pack2初始化')
```

### mod2_1.py

```python
# mod2
def func():
    print('pack2.mod2_1.func()')

if __name__ == '__main__':
    print('mod2_1 作为主程序运行')
else:
    print('mod2_1 被另一个模块调用')
```

### mod2_2.py

```python
# mod2
def func():
    print('pack2.mod2_2.func()')

if __name__ == '__main__':
    print('mod2_2 作为主程序运行')
else:
    print('mod2_2 被另一个模块调用')
```

# 2.导入（自定义）包的3种方法

我在桌面`C:\Users\Administrator\Desktop\`新建了一个`main.py`文件**（和自定义的包不在一个目录）**，**自定义包的目录：**`D:\Code_Sources\Python\Test\`

```python
import sys

# 将包含parent包的路径添加进系统路径
sys.path.append(r"D:\Code_Sources\Python\Test") 


print('-----开始import-----\n')

import parent.pack2.mod2_1          # 第1种 引用方法
import parent.pack2.mod2_2 as p2m2  # 第2种 引用方法
from parent.pack.mod import *       # 第3种 引用方法

if __name__ == '__main__':
    print('-----开始main-----\n')

    # 第1种 引用的调用方法
    parent.pack2.mod2_1.func() 
    # 第2种 引用的调用方法
    p2m2.func()
    # 第3种 引用的调用方法
    func()
    
    #  import就会把注册在包 __init__.py 文件中 __all__列表中的子模块和子包导入到当前作用域中
    print('\npack2包中的模块有：')
    print(parent.pack2.__all__)
```

**运行结果：**

```
-----开始import-----

parent 初始化
Pack2初始化
mod2_1 被另一个模块调用
mod2_2 被另一个模块调用
Pack初始化
mod 被另一个模块调用
-----开始main-----

pack2.mod2_1.func()
pack2.mod2_2.func()
pack.mod.func()

pack2包中的模块有：
['mod2_1', 'mod2_2', 'mod2_3']

请按任意键继续. . .
```

# Reference

1. [原文转载](https://cloud.tencent.com/developer/article/1596466)
2. [在Python中以绝对路径或者相对路径导入文件的方法](https://blog.csdn.net/xiongchengluo1129/article/details/80453599)