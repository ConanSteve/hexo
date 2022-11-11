---
title: Python入门
date: 2022-02-01 10:00:00
author: 陌上人如玉
---

# 入门

## 参考资料

[廖雪峰python教程](https://www.liaoxuefeng.com/wiki/1016959663602400/1017024645952992)

[cookbook](https://python3-cookbook.readthedocs.io/zh_CN/latest/index.html)

[答疑](http://c.biancheng.net/view/2380.html)

## 基础

- [f-string格式化](https://www.cnblogs.com/rgxx/p/10899440.html)

```Python
k=123.45
print(f"123:5.1f")
```

[Python 中下划线的 5 种含义 | 菜鸟教程 (runoob.com)](https://www.runoob.com/w3cnote/python-5-underline.html#:~:text=下划线前缀的含义是告知其他程序员：以单个下划线开头的变量或方法仅供内部使用。 该约定在PEP 8中有定义。 这不是Python强制规定的。 Python不像Java那样在"私有"和"公共"变量之间有很强的区别。 这就像有人提出了一个小小的下划线警告标志，说： "嘿，这不是真的要成为类的公共接口的一部分。 不去管它就好。," 如果你实例化此类，并尝试访问在__init__构造函数中定义的foo和_bar属性，会发生什么情况？ 让我们来看看： 你会看到_bar中的单个下划线并没有阻止我们"进入"类并访问该变量的值。 这是因为Python中的单个下划线前缀仅仅是一个约定 - 至少相对于变量和方法名而言。 但是，前导下划线的确会影响从模块中导入名称的方式。)

## 常用

### time

- [python求时间差](https://www.cnblogs.com/qi-yuan-008/p/12418822.html)

```Python
import time
import functools
from datetime import datetime, date

def elapse_s(func):
    @functools.wraps(func)
    def wrapper(*args, **kw):
        time1 = datetime.now()
        temp = func(*args, **kw)
        time2 = datetime.now()
        elapse = (time2-time1).microseconds/1000
        print(f"{time2}-FunctionName:{func.__name__:}-Elapse:{elapse:.3f}")
        return temp
    return wrapper

def elapse_l(func):
    @functools.wraps(func)
    def wrapper(*args, **kw):
        time1 = datetime.now()
        temp = func(*args, **kw)
        time2 = datetime.now()
        elapse = (time2-time1).microseconds/1000
        print(f"{time2}-FunctionName:{func.__name__:}-Elapse:{elapse:.3f}")
        return temp
    return wrapper

@elapse_s
def test():
    print('-----Test-----')
    time.sleep(1)

def seconds2time(seconds):
    m, s = divmod(seconds, 60)
    h, m = divmod(m, 60)
    d, h = divmod(h, 24)
    if d>0:
        return f"{d:%d}day {h:%d}:{m:%02d}:{s:%02d}"
    else:
        return f"{h:%d}:{m:%02d}:{s:%02d}"


print(seconds2time(245030.235))

```









 

# 问答

 