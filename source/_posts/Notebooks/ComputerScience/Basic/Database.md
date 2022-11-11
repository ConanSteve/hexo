---
title: 关系数据库的基本使用
date: 2022-02-01 10:00:00
author: 陌上人如玉
---

# MySQL

## 安装

[Windows 安装并配置 MySQL 5.6/5.7](https://www.cnblogs.com/alan-lin/p/9966917.html)

 [windows上同时安装两个版本的mysql数据库](https://blog.csdn.net/wudinaniya/article/details/82455431)

[mac版mysql下载地址](https://dev.mysql.com/downloads/mysql/)

### ubunut安装mysql

[手动安装mysql5.6](https://blog.csdn.net/ac_dao_di/article/details/48932729)

 [Mysql8](https://www.cnblogs.com/livelab/p/12808150.html)

 [如何从命令行管理MySQL数据库和用户](https://www.iplayio.cn/post/9225021)

 [安装MariaDB](https://www.cnblogs.com/lzwangshubo/p/9977997.html)

[Mysql-mysql8创建用户用户并授权-远程访问](https://blog.csdn.net/silence_xiang/article/details/103472888)

 [远程主机无法访问](https://www.cnblogs.com/xiaojf/p/11107934.html)

 [修改字符集](https://blog.csdn.net/yeya24/article/details/81836218)

## 管理Mysql

### 创建用户

```sql
create user if NOT EXISTS 'fan'@'%' identified by '12121212';
flush privileges;
```

### 修改用户密码

```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'fanfan';
```

###  授予数据库权限

```sql
GRANT ALL PRIVILEGES ON **.** TO 'fan'@'%';
```

5.5本地访问需要单独添加localhost权限

```sql
grant all on *.* to fan@localhost; 
flush privileges; 
```

### 访问数据库

```
mysql -h 172.18.32.92 -u root -p
```

### 授予用户管理指定数据库权限 

```sql
GRANT ALL PRIVILEGES ON databaseName.* TO 'zhuanzhi_shuqi'@'%';
```



# Reference

[https://www.cnblogs.com/hxlinux/p/12900503.html]

[查看mysql数据库是否存在某张表及某张表是否存在某个字段](https://www.cnblogs.com/yaradish/p/10078640.html)