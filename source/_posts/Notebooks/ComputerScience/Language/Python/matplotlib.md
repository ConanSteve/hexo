---
title: matplotlib
date: 2022-02-01 10:00:00
author: 陌上人如玉
categories:
  [编程语言, Python]
---

## 绘制曲线图

```Python
import matplotlib.pyplot as plt

train_losses, train_accuracy = [], []
val_losses, val_accuracy = [], []
for epoch in range(1, 20):
    epoch_loss, epoch_accuracy = fit(epoch, model, train_loader, phase='training')
    val_epoch_loss, val_epoch_accuracy = fit(epoch, model, test_loader, phase='validation')
    train_losses.append(epoch_loss)
    train_accuracy.append(epoch_accuracy)
    val_losses.append(val_epoch_loss)
    val_accuracy.append(val_epoch_accuracy)

plt.plot(range(1, len(train_losses) + 1), train_losses, marker="o", color="blue", label='training loss')
plt.plot(range(1, len(val_losses) + 1), val_losses, 'r', label='validation loss')
plt.legend() 
plt.show()
plt.plot(range(1, len(train_accuracy) + 1), train_accuracy, 'bo', label='train accuracy')
plt.plot(range(1, len(val_accuracy) + 1), val_accuracy, 'r', label='val accuracy')
plt.legend()
plt.show()
```

[Matplotlib - 折线图 plot() 所有用法详解](https://blog.csdn.net/weixin_40683253/article/details/87376085)

[matplotlib.pyplot.plot()参数详解](https://blog.csdn.net/sinat_36219858/article/details/79800460)

[官方资料](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.plot.html)

### 绘制正余弦

```Go
import matplotlib.pyplot as plt
import math

x_len = 50
train_losses = [math.sin(i/x_len*2*math.pi) for i in range(x_len)]
val_losses = [math.cos(i/x_len*2*math.pi) for i in range(x_len)]

plt.plot(range(1, len(train_losses) + 1), train_losses,marker="o", color="blue", lineStyle="-", label='training loss')
plt.plot(range(1, len(val_losses) + 1), val_losses, color="red", label='validation loss')
plt.legend()
plt.show()
```