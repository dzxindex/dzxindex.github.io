---
layout: post
title: sqlmap 使用
categories: [安全工具]
description: sqlmap
keywords: 安全工具,sqlmap
---

# sqlmap 


sqlmap is an open source penetration testing tool that automates the process of detecting and exploiting SQL injection flaws and taking over of database servers. It comes with a powerful detection engine, many niche features for the ultimate penetration tester, and a broad range of switches including database fingerprinting, over data fetching from the database, accessing the underlying file system, and executing commands on the operating system via out-of-band connections.

## 下载地址

sqlmap 下载地址：

```
git clone --depth 1 https://github.com/sqlmapproject/sqlmap.git sqlmap-dev
```

##

```
sqlmap -u "http://www.xx.com/username/admin*"       #如果我们已经知道admin这里是注入点的话，可以在其后面加个*来让sqlmap对其注入
```

## 深入了解 SQLMAP API

SQLMAP API 命令和二次开发

https://www.freebuf.com/articles/web/204875.html

