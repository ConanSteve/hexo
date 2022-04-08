---
title: pymysql的基本用法
date: 2022-04-08
author: 陌上人如玉
comments:
description: python如何连接、增删改查mysql数据库
keywords:
top_img:
cover:
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
tags: mysql
categories: Python
---

# 安装pymysql

```shell
pip install pymysql
```

# 连接数据库

```python
db = pymysql.connect(IP_address, username, password, database_name)
```

参数说明：

* IP_address：数据库IP地址，本地可以为`localhost`
* username：数据库用户名
* password：数据库用户名对应的密码
* database_name：要连接的数据库名称

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



# Template

下面的包直接进一步封装了pymysql包，根据个人需求可以自己更改

```python
# import mysql.connector
#
# # 注意把password设为你的root口令:
# conn = mysql.connector.connect(user='root', password='password', database='zhitu')
# cursor = conn.cursor()
# # 创建user表:
# cursor.execute('create table user (id varchar(20) primary key, name varchar(20))')
# # 插入一行记录，注意MySQL的占位符是%s:
# cursor.execute('insert into user (id, name) values (%s, %s)', ['1', 'Michael'])
# cursor.rowcount
#
# conn.commit()
# cursor.close()
# # 运行查询:
# cursor = conn.cursor()
# cursor.execute('select * from user where id = %s', ('1',))
# values = cursor.fetchall()
# values
# [('1', 'Michael')]
# # 关闭Cursor和Connection:
# cursor.close()
# True
# conn.close()

import pymysql, os, json



class MySQL:
    def __init__(self):
        # 打开数据库连接
        self.db = pymysql.connect("localhost", "root", "123", "新冠backup")
        # 使用 cursor() 方法创建一个游标对象 cursor
        self.cursor = self.db.cursor()

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

    def query(self, command, params=None):
        result = self.cursor.execute(command, params)
        # 使用 fetchone() 方法获取单条数据.
        data = self.cursor.fetchmany(result)
        return data

    def commit(self):
        self.db.commit()

    def close(self):
        self.cursor.close()
        self.db.close()

        
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

