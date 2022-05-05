---
layout: post
title: 逆向 APP 学习-01-oulapp的双向证书破解
categories: [逆向]
description: oulapp的双向证书破解
keywords:  反编译,逆向
---

# 使用工具

[jadx](https://github.com/skylot/jadx/releases)

# 定位
下载一个app（豌豆荚下载最新版），然后在资源文件里面找cer或者p12证书文件。
直接找到，省了很多事。。。。 然后我们要继续看它的证书密码了，这个先来逆向反编译看一看。然后我们全局搜他的关键词client.cer（我这里用的是 [jadx](https://github.com/skylot/jadx/releases) ）。


# 转载
https://juejin.cn/post/6844904084630142984

https://blog.csdn.net/qq_38316655/article/details/104176882


https://blog.yii2.cc/mutual-tls-authentication/

https://github.com/Kenny1993/soulapp