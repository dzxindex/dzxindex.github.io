---
layout: post
title: Fastjson 远程命令执行进阶
categories: [安全漏洞]
description: Fastjson 远程命令执行进阶

keywords: 安全漏洞, fastjson
---

# 环境构建

[配置任意版本 fastjson 环境
](https://github.com/dzxindex/JNDI-Injection-Bypass)

# 进阶 payload

payload:
https://www.freebuf.com/articles/web/283585.html


fastjson 反序列化漏洞整理：
http://x2y.pw/2020/11/15/fastjson-%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96%E6%BC%8F%E6%B4%9E%E6%95%B4%E7%90%86/


https://paper.seebug.org/papers/scz/web/202005121629.txt

Fastjson姿势技巧集合:
https://github.com/safe6Sec/Fastjson

最全fastjson漏洞复现与绕过:
https://cloud.tencent.com/developer/article/1974944

Fastjson之源码分析：
https://www.cnblogs.com/nice0e3/p/14601670.html#fastjson%E4%BD%BF%E7%94%A8


[源码分析 fastjson 
](https://www.cnblogs.com/nice0e3/p/14601670.html#fastjson%E6%A6%82%E8%BF%B0)

[fastjson反序列化笔记
](https://apsry.github.io/2022/03/10/fastjson/)

[fastjson_rec_exploit](https://github.com/mrknow001/fastjson_rec_exploit)

[Fastjson姿势技巧集合](https://github.com/safe6Sec/Fastjson)

[fastjson 不出网利用总结
](https://cloud.tencent.com/developer/article/1785575)

[FastjonExploit | Fastjson漏洞快速利用框架
](https://github.com/c0ny1/FastjsonExploit)


# 工具
[JNDI-Injection-Exploit
](https://github.com/welk1n/JNDI-Injection-Exploit/blob/master/README-CN.md)

[fastjson漏洞burp插件，检测fastjson<1.2.68基于dnslog，fastjson<=1.2.24和1.2.33<=fatjson<=1.2.47的不出网检测和TomcatEcho,SpringEcho回显方案。](https://github.com/zilong3033/fastjsonScan)

[fastjson不出网利用、c3p0](https://github.com/depycode/fastjson-c3p0)
[fastjson 被动扫描、不出网payload生成
](https://github.com/bigsizeme/fastjson-check)


# 环境条件查询

java 版本：
```
java -version
```

> 编译（关于Javac环境，测试机与靶机一定要接近，否则无法.class文件无法被正常解析执行）


