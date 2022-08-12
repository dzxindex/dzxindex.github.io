---
layout: post
title: ctfhub-文件上传
categories: [CTF]
description: ctfhub
keywords: ctfhub 
---

# 工具地址

[冰蝎](https://github.com/rebeyond/Behinder/releases)

## 什么是PHP木马


经典一句话木马大多都是只有两个部分，一个是可以执行代码的函数部分，一个是接收数据的部分。

例如：**<?php eval(@$_POST['a']); ?>**

其中eval就是执行命令的函数，**$_POST['a']**就是接收的数据。eval函数把接收的数据当作PHP代码来执行。这样我们就能够让插入了一句话木马的网站执行我们传递过去的任意PHP语句。这便是一句话木马的强大之处。