---
layout: post
title: 快速配置环境
categories: 快速配置环境
description: 快速配置环境
keywords: 快速配置环境
---

# go 环境

```
wget -c https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz

tar -C  /usr/local  -zxf go1.8.3.linux-amd64.tar.gz

vim /etc/profile
:export PATH=$PATH:/usr/local/go/bin
 source /etc/profile
 go version
```