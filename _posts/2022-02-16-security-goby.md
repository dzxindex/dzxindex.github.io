---
layout: post
title: 网络安全渗透测试使用 goby 检测 log4j 漏洞
categories: [安全]
description: goby 扫描器使用方式
keywords:  安全
---

# goby 

Goby 是通过 golang 编写的扫描器

下载链接:

https://cn.gobies.org/#dl



## 一、前言

前段时间的Log4j漏洞影响很广泛，网上已经公开了很多地方的利用方式，而平时用goby较多，就想利用goby的指纹识别对目标定向检测。这篇文章就从Apache Solr Log4j漏洞为例，教大家如何写goby poc，文章中有错误还请及时指正。

Goby可以通过编写go文件，来实现一些高级的漏洞检测或利用，例如dnslog检测漏洞，详情可查阅goby官方文档：https://cn.gobies.org/docs/exp/index.html



## 二、漏洞復現





## 三、goby poc 编写

Goby 是通过 golang 编写的，而一些漏洞检测场景（比如dnslog验证），goby自身的JSON 格式无法满足这一需求，需采用 Golang 编写漏洞代码。



