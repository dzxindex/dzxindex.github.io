---
layout: post
title: Docker 搭建 awes 和 nessus
categories: [正则]
description: 正则
keywords:  
---

# 什么是 nessus ？

## nessus 官网安装



查对应 linux 版本 https://www.tenable.com/downloads/nessus?loginAttempted=true 下载对应版本的 nessus 程序：

> 下载安装包 Nessus-10.1.1-ubuntu1110_amd64.deb

## nessus docker 版本安装


1. 运行docker 版本
```
docker run -it -d \
   -p 3443:3443 \
   -p 8834:8834 \
   --name=leishi \
   leishianquan/awvs-nessus:v4
```
2. 运行 nessusd
  

/etc/init.d/nessusd start 

3. 访问扫描器地址和账号密码

```
Nessus:
https://127.0.0.1:8834/#/
account: leishi / leishianquan

Awvs13:
https://127.0.0.1:13443/
account: leishi@leishi.com / Leishi123
```

##  更新插件 

下载插件：


更新插件
```
 /opt/nessus/sbin/nessuscli update all-2.0.tar.gz
```

重启
```
/etc/init.d/nessusd stop
/etc/init.d/nessusd start

```
## 参考

[破解插件](https://www.ddosi.org/nessus-pro/)

https://blog.zygd.site/Docker%E6%90%AD%E5%BB%BAawes%E5%92%8Cnessus.html#%E5%85%B3%E4%BA%8E%E5%90%AF%E5%8A%A8%E5%91%BD%E4%BB%A4%EF%BC%9A