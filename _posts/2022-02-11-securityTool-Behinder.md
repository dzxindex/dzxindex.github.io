---
layout: post
title: 冰蝎使用
categories: [安全工具]
description: sqlmap
keywords: 安全工具,sqlmap
---

# 一．启动

![](https://img-blog.csdnimg.cn/20210303104648896.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JyaW5nX2NvY28=,size_16,color_FFFFFF,t_70)
Windows环境下：

[java 安装包下载](https://www.java.com/zh-TW/download/)

1.配置环境：冰蝎只支持 **jre6-jre8**
可以在电脑上查看java版本
命令：java -version

2.启动

在冰蝎目录下命令行输入
命令：`java -jar Behinder.jar`（这里文件名可简化）

即可开启
Linux环境下：
注意切换jdk版本6-8，对应javac版本也要和java版本相同，同理打开冰蝎目录输入命令


![](https://img-blog.csdnimg.cn/20210303104505862.png)


二．使用（在本机进行实测）

1. 配置PHP环境

2. 在网站根目录下创建一个shell2.php的php文件，文件内容需要我们下载的冰蝎server中带有的shell.php文件中的内容复制过去
   
![](https://img-blog.csdnimg.cn/20210303104623711.png)
![](https://img-blog.csdnimg.cn/20210303104635231.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JyaW5nX2NvY28=,size_16,color_FFFFFF,t_70)


![](https://img-blog.csdnimg.cn/20210303104639653.png)

可以看到默认连接密码为 rebeyond
这时通过冰蝎去连接该文件


![](https://img-blog.csdnimg.cn/20210303104648896.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JyaW5nX2NvY28=,size_16,color_FFFFFF,t_70)

输入URL和密码即可

![](https://img-blog.csdnimg.cn/20210303104659769.png)

点击此URL

![](https://img-blog.csdnimg.cn/20210303104710853.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JyaW5nX2NvY28=,size_16,color_FFFFFF,t_70)

可以看到成功连接，此时已经把基本信息显示出来了

三．模块介绍

### 1.基本信息
直接显示出phpinfo，通过此表可以用来信息收集

### 2.命令执行

![](https://img-blog.csdnimg.cn/20210303104751611.png)

### 3.虚拟终端

![](https://img-blog.csdnimg.cn/20210303104805531.png)

也可以进行cmd.exe，powershell.exe等功能

4.文件管理

## 转载


https://blog.csdn.net/bring_coco/article/details/114302178