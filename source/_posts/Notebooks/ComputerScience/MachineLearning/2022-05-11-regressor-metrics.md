---
title: 机器学习笔记之回归模型
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
tags: MachineLearning
categories: 
    机器学习笔记
  
---

## 模型
### lightGBM
[sklearn与LightGBM配合使用](https://blog.csdn.net/qq_38319401/article/details/104360617)
```python
# coding: utf-8
import lightgbm as lgb
import pandas as pd
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import GridSearchCV

# 加载数据
print('加载数据...')
df_train = pd.read_csv('./data/regression.train.txt', header=None, sep='\t')
df_test = pd.read_csv('./data/regression.test.txt', header=None, sep='\t')

# 取出特征和标签
y_train = df_train[0].values
y_test = df_test[0].values
X_train = df_train.drop(0, axis=1).values
X_test = df_test.drop(0, axis=1).values

print('开始训练...')
# 直接初始化LGBMRegressor
# 这个LightGBM的Regressor和sklearn中其他Regressor基本是一致的
gbm = lgb.LGBMRegressor(objective='regression',
                        num_leaves=31,
                        learning_rate=0.05,
                        n_estimators=20)

# 使用fit函数拟合
gbm.fit(X_train, y_train,
        eval_set=[(X_test, y_test)],
        eval_metric='l1',
        early_stopping_rounds=5)

# 预测
print('开始预测...')
y_pred = gbm.predict(X_test, num_iteration=gbm.best_iteration_)
# 评估预测结果
print('预测结果的rmse是:')
print(mean_squared_error(y_test, y_pred) ** 0.5)
```
[lgb.LGBMRegressor参数解释以及调参方法](https://www.pythonheidong.com/blog/article/468277/6e714898cdbbb5af9979/)
## 评价指标
[回归评价指标](https://www.cnblogs.com/nxf-rabbit75/p/10415812.html)
