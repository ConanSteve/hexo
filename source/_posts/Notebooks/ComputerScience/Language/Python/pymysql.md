---
title: pymysql的基本用法
date: 2022-04-08
author: 陌上人如玉
comments:
description: python如何连接、增删改查mysql数据库
keywords: pymysql
top_img:
cover:
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
tags: mysql
categories:
  [编程语言, Python]
---

# 安装pymysql

```shell
pip install pymysql
```

# 连接数据库

```python
db = pymysql.connect(host=IP_address, user=username, password=password, database=database_name, charset="utf8")
```

参数说明：

* host：数据库IP地址，本地可以为`localhost`
* user：数据库用户名
* password：数据库用户名对应的密码
* password：要连接的数据库名称

# 增删改查

操作都要通过一个游标执行，所以，创建连接的时候，直接创建一个cursor

```python
cursor = db.cursor()
```

## 执行语句

```python
cursor.execute(command, params=None)
```

参数说明：

* `command`：str类型，sql语句字符串
* `params`：tuple类型，当command使用占位符`%s`时，可传入占位符对应的字符值

# 关闭数据库连接

```python
cursor.close() # 需要先关闭游标
db.close() 
```



# 实例说明

## 测试环境

* 数据库版本：5.6.41
* 系统：MacOS 10.13.6

下面的数据库被用来作实例说明

创建脚本

```sql
/*
 Navicat Premium Data Transfer

 Source Server         : 127.0.0.1-root
 Source Server Type    : MySQL
 Source Server Version : 50641
 Source Host           : localhost:3306
 Source Schema         : test

 Target Server Type    : MySQL
 Target Server Version : 50641
 File Encoding         : 65001

 Date: 08/04/2022 20:03:35
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for user
-- ----------------------------
DROP TABLE IF EXISTS `user`;
CREATE TABLE `user` (
  `id` varchar(12) NOT NULL,
  `username` varchar(255) DEFAULT NULL,
  `age` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

-- ----------------------------
-- Records of user
-- ----------------------------
BEGIN;
INSERT INTO `user` VALUES ('id_001', 'Tom', 23);
INSERT INTO `user` VALUES ('id_002', 'Jack', 25);
INSERT INTO `user` VALUES ('id_003', 'Rose', 18);
COMMIT;

SET FOREIGN_KEY_CHECKS = 1;
```

![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204081959090.png)

### 连接数据库


```python
import pymysql
db = pymysql.connect(host="localhost", user="root", password="", database="test")
cursor= db.cursor()
```

### 查询

查询返回的数据为二维tuple类型


```python
cmd = "select * from user"
result=cursor.execute(cmd)
data = cursor.fetchmany(result)
for _ in data: print(_)
```

​    ('id_001', 'Tom', 23)
​    ('id_002', 'Jack', 25)
​    ('id_003', 'Rose', 18)


### 增加数据


```python
cmd = "insert into `user` values (%s,%s,%s)"
param=("id_004", "Lucy", str(21))
r = cursor.execute(cmd, param)
print(r)
cmd = "select * from user"
result=cursor.execute(cmd)
data = cursor.fetchmany(result)
for _ in data: print(_)
```

​    1
​    ('id_001', 'Tom', 23)
​    ('id_002', 'Jack', 25)
​    ('id_003', 'Rose', 18)
​    ('id_004', 'Lucy', 21)


### 删除数据库


```python
cmd = "delete from user where username=%s"
param=("Lucy",)
r = cursor.execute(cmd, param)
print(r)
cmd = "select * from user"
result=cursor.execute(cmd)
data = cursor.fetchmany(result)
for _ in data: print(_)
```

​    1
​    ('id_001', 'Tom', 23)
​    ('id_002', 'Jack', 25)
​    ('id_003', 'Rose', 18)


### 关闭数据库连接


```python
cursor.close()
db.close()
```

### 提交数据库

对数据库做了改变之后，必须提交，否则数据库不会更新

```python
db.commit()
```



# 封装

下面的包直接进一步封装了pymysql包，根据个人需求可以自己更改

```python
import pymysql, os, json

class MySQL:
    def __init__(self):
        # 打开数据库连接
        self.db = pymysql.connect(host = "localhost",
                                  user = "root", 
                                  password = "", 
                                  database = "test")
        # 使用 cursor() 方法创建一个游标对象 cursor
        self.cursor = self.db.cursor()
        self.open = True
        print("数据库连接成功！ connect database succeed!")

    def connect(self):
        pass

    def execute(self, command, params=None):
        # 使用 execute()  方法执行 SQL 查询
        r = None
        if params is None:
            r = self.cursor.execute(command)
        else:
            r = self.cursor.execute(command, params)
        return r
      
		#  返回的是一个二维的tuple
    def query(self, command, params=None):
        result = self.cursor.execute(command, params)
        # 使用 fetchone() 方法获取单条数据.
        data = self.cursor.fetchmany(result)
        return data

    def commit(self):
        self.db.commit()

    def close(self):
      	if self.open:
          self.cursor.close()
          self.db.close()
          self.open = False
          print("数据库成功关闭！")
        
    def __del__(self):
      	self.close()

        
def main():
    sql = MySQL()
    # cmd = "select * from person where code =12345"
    # r = sql.query(cmd)
    # import_customers(sql)
    r= sql.query("show tables")
    print(r)
    sql.close()
    print("completed!")


if __name__ == '__main__':
    main()

```



# Reference

1. [pymysql的基本使用](https://www.cnblogs.com/xfxing/p/9322199.html)
