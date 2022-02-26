---
layout: post
title: 网络安全渗透测试使用 goby 检测 log4j 漏洞
categories: [安全]
description: goby 扫描器使用方式
keywords:  安全
---

# goby 

Goby 是通过 golang 编写的扫描器，同时拥有资产扫描、资产识别和漏洞扫描能力，安装简单，直接解压即可使用，界面也非常友好，内置了大量由官方和其他网络安全从业者提供的poc。

下载链接:

https://github.com/gobysec/Goby/releases



## 前言

前段时间的Log4j漏洞影响很广泛，网上已经公开了很多地方的利用方式，而平时用goby较多，就想利用goby的指纹识别对目标定向检测。这篇文章就从Apache Solr Log4j漏洞为例，教大家如何写goby poc，文章中有错误还请及时指正。

Goby可以通过编写go文件，来实现一些高级的漏洞检测或利用，例如dnslog检测漏洞，详情可查阅goby官方文档：https://cn.gobies.org/docs/exp/index.html

## 准备知识

[ 添加 goby poc 教程](https://github.com/gobysec/Goby/wiki/Vulnerability-writing-guide#goby-%E6%BC%8F%E6%B4%9E%E6%89%AB%E6%8F%8F%E5%BC%95%E6%93%8E%E6%A8%A1%E6%9D%BF%E4%BB%8B%E7%BB%8D)

## 二、漏洞復現





## 三、goby poc 编写

Goby 是通过 golang 编写的，而一些漏洞检测场景（比如dnslog验证），goby自身的JSON 格式无法满足这一需求，需采用 Golang 编写漏洞代码。



### expJson部分



1、首先通过goby poc管理，添加poc，按照goby官方漏洞描述模版说明填写并保存。

![img](https://p3.ssl.qhimg.com/t010bfe776910c3633b.jpg)



2、在 goby 安装目录的\golib\exploits\user 文件夹打开生成的Apache_Solr_Log4j_JNDI_RCE.json文件，如果不需要 exp 则需把 HasExp 字段的 true 改为 false。







