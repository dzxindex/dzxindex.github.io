---
layout: post
title: FOFA介绍
categories: [FOFA, 信息收集]
description: FOFA是一款非常强大的搜索引擎
keywords: FOFA , 信息收集
---


# FOFA介绍


[FOFA](https://fofa.so/) 是一款非常强大的搜索引擎，FOFA（网络空间资产检索系统）是世界上数据覆盖更完整的IT设备搜索引擎，拥有全球联网IT设备更全的DNA信息。

## FOFA基础语法

### 1. title网站标题

title="beijing" 从标题中搜索“北京”

### 2. body页面内容

body可以通过页面中包含的特定字符串来搜索资产。

### 3. domain域名

搜索域名中包含http://xuegod.cn的资产，此方法相当于子域名的搜索。

domain="http://xuegod.cn"


### 4. 地区搜索
country="CN" 搜索指定国家(编码)的资产。

region="Xinjiang" 搜索指定行政区的资产

city="beijing" 搜索指定城市的资产。

排除地区方法使用 !=

country="CN" 搜索指定国家(编码)的资产。

region="Xinjiang" 搜索指定行政区的资产

city="beijing" 搜索指定城市的资产。

排除地区方法使用 !=

## 漏洞搜索

举个例子：
Apache solr XML 实体注入漏洞

fofa搜索：

```
app="Solr" && port="8983"
```