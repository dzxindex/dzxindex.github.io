---
layout: post
title: Cobalt Strike汉化版——安装与使用教程
categories: 安全工具
description: Cobalt Strike汉化版——安装与使用教程
keywords: cs
---


## 一、CS简单介绍


Cobalt Strike是一个为对手模拟和红队行动而设计的平台，主要用于执行有目标的攻击和模拟高级威胁者的后渗透行动。
分为服务器和客户端，方便团队合作。

**个人理解：**
cs服务器部署在公网控制着受害者主机，而攻击者可以直接访问cs服务器进而控制受害主机，不用再通过端口转发使用msf控制受害主机，简单方便！

![](https://img-blog.csdnimg.cn/20210409161134252.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)


## 二、安装启动教程

**环境要求**
1、客户端，服务端都需要Java环境
2、服务端必须安装在Linux系统上

**示例：**
cs服务端：kaili2020
cs客户端：win10

**cs服务端安装启动**

原版未汉化下载 cs4.0 百度云盘：https://pan.baidu.com/s/1k4GY0IAHzdkd6PysYFxe5w，提取码：rymo
汉化版放在了我的知识星球与我的资源中

下载完cs4.0之后，将文件夹复制到 kali
执行teamserver文件，即可安装启动cs服务端

```
./teamserver 192.168.184.145（kali的IP） 123（密码随便设）
```

如下图所示即是成功启动 cs 服务端

![](https://img-blog.csdnimg.cn/202104091618104.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)



