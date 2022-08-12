---
layout: post
title: ctf hub
categories: [shortcut]
description: ctf hub
keywords: ctf 
---

#

## 信息泄露


### Git泄露

#### Stash


``` shell
git stash list 查看保存的工作现场列表    
git stash pop 恢复工作现场    
git stash show 显示做了哪些改动  
git stash show -p 显示第一个保存的工作现场的改动  
```


### SVN泄露

检测工具： 

- `dvcs-ripper`


#### 选择 docker 运行

https://github.com/kost/dvcs-ripper.git

```
# 下载结果
docker run  -it -v /tmp:/work:rw  k0st/alpine-dvcs-ripper rip-svn.pl -v -u http://challenge-93c154a7ce270916.sandbox.ctfhub.com:10800/.svn/
```
> docker -v  映射目录


### HG泄露

HG Mercurial 版本控制系统


访问下载/.hg/store/fncache文件


## 密码口令


### 弱密码爆破

burpsuit 简单密码爆破
https://cloud.tencent.com/developer/article/1510007

## SQL注入

参考连接： https://www.jianshu.com/p/a5f47e991566
### 整数型注入
