---
layout: post
title: getshell 常见实战
categories: [ 安全学习]
description: getshell
keywords: 安全学习 
---

# getshell

## 一次对跨境赌博类APP的渗透实战

[一次对跨境赌博类APP的渗透实战](https://mp.weixin.qq.com/s?__biz=Mzg2NDYwMDA1NA==&mid=2247485589&idx=1&sn=f4f64ea923675c425f1de9e4e287fb07&chksm=ce67a20cf9102b1a1a171041745bd7c243156eaee575b444acc62d325e2cd2d9f72b2779cf01&scene=21#wechat_redirect)

### 本次渗透实战主要知识点：

1.app抓包，寻找后台地址

2.上传绕过，上传shell

3.回shell地址的分析

4.中国蚁剑工具的运用

### 使用工具

#### fuzz 是什么，它有什么用？

[fuzz测试简介](https://xz.aliyun.com/t/9022)

[WFUZZ](https://blog.csdn.net/JBlock/article/details/88619117)

web fuzz 模糊测试工具

[American Fuzzy Lop](https://blog.csdn.net/aperture1/article/details/113834050)
一款 fuzz 模糊测试工具


## 记一次后门爆破到提权实战案例

[记一次后门爆破到提权实战案例](https://mp.weixin.qq.com/s?__biz=Mzg2NDYwMDA1NA==&mid=2247485647&idx=2&sn=28a227ff21a6a99e323f6e27130a5ad5&chksm=ce67a256f9102b4030db2fc636ff1d454d46178fc2003368305cdc06ae2a4c81dd011dfcb361&scene=21#wechat_redirect)

## 思路

- 御剑对目标站的旁站进行扫描
- 旁站提权进入(MS12-042提权EXP成功)

> 注：可以用netstat -ano、tasklist命令来查看目标机器中是否安装的有可用于提权的第三方软件，如：Radmin、Gene6FTP、FileZilla Server等。

[御剑](https://github.com/foryujian/yjdirscan)

### 爆破字典

[爆破字典 demo01](https://github.com/3had0w/Fuzzing-Dicts)