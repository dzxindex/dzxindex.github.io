---
layout: post
title: Python程序中设置HTTP代理
categories: 工具类
description: 快速安装 docker
keywords: docker
---

## 

[原文地址：
](https://zhuanlan.zhihu.com/p/30787723)

本文主要给大家简单讲解了下http代理的概念以及如何在Python程序中设置http代理的方法，非常的详细，有需要的小伙伴可以参考下

#  HTTP_PROXY / HTTPS_PROXY 环境变量

urllib2 和 Requests 库都能识别 HTTP_PROXY 和 HTTPS_PROXY 环境变量，一旦检测到这些环境变量就会自动设置使用代理。这在用HTTP代理进行调试的时候非常有用，因为不用修改代码，可以随意根据环境变量来调整代理服务器的ip地址和端口。*nix中的大部分软件也都支持HTTP_PROXY环境变量识别，比如curl、wget、axel、aria2c等

```dotnetcli
$ http_proxy=121.193.143.249:80 python -c 'import requests; print(requests.get("http://httpbin.org/ip").json())'
{u'origin': u'121.193.143.249'}

$ http_proxy=121.193.143.249:80 curl httpbin.org/ip
{
 "origin": "121.193.143.249"
}
```

```dotnetcli
In [245]: os.environ['http_proxy'] = '121.193.143.249:80'
In [246]: requests.get("http://httpbin.org/ip").json()
Out[246]: {u'origin': u'121.193.143.249'}
In [249]: os.environ['http_proxy'] = ''
In [250]: requests.get("http://httpbin.org/ip").json()
Out[250]: {u'origin': u'x.x.x.x'}
```

```dotnetcli
import requests
import os


os.environ['http_proxy'] = '192.168.22.2:1088'
os.environ['https_proxy'] = '192.168.22.2:1088'
r = requests.get("http://httpbin.org/ip").json()
print(r)
r = requests.get("http://www.google.com/")
print(r)

```
# requests 模块使用代理
```al
import requests
proxy = {
'http' : 'http://138.197.222.35:80',
'https' : 'http://1138.197.222.35:8080'
}

r = requests.get('http://httpbin.org/ip', proxies=proxy)
print (r)

```

# 查看请求来源地址网址
```nginx

 curl httpbin.org/ip
```