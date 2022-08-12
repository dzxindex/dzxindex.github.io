---
layout: post
title: Cobalt Strike 的安装与使用教程
categories: 安全工具
description: Cobalt Strike 汉化版的安装与使用教程
keywords: cs
---


## 一、CS简单介绍


Cobalt Strike是一个为对手模拟和红队行动而设计的平台，主要用于执行有目标的攻击和模拟高级威胁者的后渗透行动。
分为服务器和客户端，方便团队合作。

**个人理解：**
cs服务器部署在公网控制着受害者主机，而攻击者可以直接访问cs服务器进而控制受害主机，不用再通过端口转发使用msf控制受害主机，简单方便！

![](https://img-blog.csdnimg.cn/20210409161134252.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)


## 二、安装启动教程

**环境要求**

1、客户端，服务端都需要 `Java环境`

2、服务端安装在 `Linux系统 `上

**示例：**
cs服务端：kaili2020
cs客户端：win10

**cs服务端安装启动**

原版未汉化下载 cs4.0 百度云盘：https://pan.baidu.com/s/1k4GY0IAHzdkd6PysYFxe5w，提取码：rymo
汉化版放在了我的知识星球与我的资源中

下载完cs4.0之后，将文件夹复制到 kali
执行teamserver文件，即可安装启动cs服务端

```
./teamserver <服务器ip地址> <密码>
```

如下图所示即是成功启动 cs 服务端

![](https://img-blog.csdnimg.cn/202104091618104.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)


**cs客户端安装启动**
双击cs4.0文件夹中的 cobaltstrike.exe 即可成功启动cs
![](https://img-blog.csdnimg.cn/20210409162525115.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)


```

host：cs服务端地址
port：端口默认不变
user：用户名随便写
Password：123（服务端启动时输入的密码）
之后点击Connect即可

```

![](https://img-blog.csdnimg.cn/20210409162620125.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)


cs客户端成功启动后如下图所示

![](https://img-blog.csdnimg.cn/20210409162817576.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)


## 三、Cobalt Strike 菜单介绍

**1、Cobalt Strike**

```

New Connection      #新建连接，支持连接多个服务器端
Preferences         #设置Cobal Strike界面、控制台、以及输出报告样式、TeamServer连接记录
Visualization       #主要展示输出结果的视图
VPN Interfaces      #设置VPN接口
Listenrs            #创建监听器
script Manager      #脚本管理，可以通过Aggressorscripts脚本来加强自身，能够扩展菜单栏，Beacon命令行，提权脚本等
close               #退出连接
```

**2、View**
```
Applications         #显示受害主机的应用信息
Credentials          #显示所有以获取的受害主机的凭证，如hashdump、Mimikatz
Downloads            #查看已下载文件
Event Log            # 主机上线记录以及团队协作聊天记录
Keystrokes           #查看键盘记录结果
Proxy Pivots         #查看代理模块
Screenshots          #查看所有屏幕截图
Script Console       #加载第三方脚本以增强功能
Targets              #显示所有受害主机
Web Log              #所有Web服务的日志
```

**3、Attacks**

**LPackages**:

```

HTML Application       #生成(executable/VBA/powershell)这三种原理实现的恶意木马文件
MS Office Macro        #生成office宏病毒文件
Payload Generator      #生成各种语言版本的payload
Windows Executable     #生成可执行exe木马
Windows Executable(S)  #生成无状态的可执行exe木马

```

**Web Drive-by:**
```
Manage                 #对开启的web服务进行管理
Clone Site             #克隆网站，可以记录受害者提交的数据
Host File              #提供文件下载，可以选择Mime类型
Scripted Web Delivery  #为payload提供web服务以便下载和执行，类似于Metasploit的web_delivery
Signed Applet Attack   #使用java自签名的程序进行钓鱼攻击(该方法已过时)
```


**Spear Phish #鱼叉钓鱼邮件**


**4、Reporting**
```
Activity Report                       #活动报告
Hosts Report                          #主机报告
Indicators of Compromise              #IOC报告：包括C2配置文件的流量分析、域名、IP和上传文件的MD5 hashes
Sessions Report                       #会话报告
Social Engineering Report             #社会工程报告：包括鱼叉钓鱼邮件及点击记录
Tactics, Techniques, and Procedures   #战术技术及相关程序报告：包括行动对应的每种战术的检测策略和缓解策略
Reset Data                            #重置数据
Export Data                           #导出数据，导出.tsv文件格式
```

**5、Help**
```
Homepage            #官方主页 
Support             #技术支持 
Arsenal             #开发者 
System information  #版本信息 
About               #关于
```
工具栏说明
![](https://img-blog.csdnimg.cn/2021041213283838.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)

## 四、使用教程


使用大致流程
创建团队服务器->客户端连接服务器->创建监听器->生成后门对应监听器->靶机运行后门成功上线->后渗透（提权，内网漫游，域渗透等)

**1、创建监听器**
如下图所示

![](https://img-blog.csdnimg.cn/20210412133526142.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)


之后点击添加

![](https://img-blog.csdnimg.cn/20210412133553510.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)


![](https://img-blog.csdnimg.cn/20210412133850833.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)

出现下图弹窗则说明监听器设置成功，并且正在监听

![](https://img-blog.csdnimg.cn/20210412133903839.png)


**2、生成木马**
按下图所示生成Windows Executable后门木马

![](https://img-blog.csdnimg.cn/20210412134251445.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)

选择已生成好的监听器

![](https://img-blog.csdnimg.cn/20210412134438131.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)


勾选X64：目标系统是64位的话需要勾选

![](https://img-blog.csdnimg.cn/20210412134500941.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)

将生成的木马保存在电脑中
![](https://img-blog.csdnimg.cn/20210412134533811.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)
保存成功后会有如下提示

![](https://img-blog.csdnimg.cn/2021041213455115.png)


**3、执行木马、反弹会话**

**前提条件：**假设已成功植入webshell，并且通过webshell上传了后门木马artifact.exe

*靶机*： win7 IP：192.168.184.141
_使用蚁剑连接webshell_

![](https://img-blog.csdnimg.cn/20210412141515415.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)


![](https://img-blog.csdnimg.cn/20210412141554121.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)


执行artifact.exe后门文件，目标靶机成功上线

![](https://img-blog.csdnimg.cn/20210412141713287.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)

点击查看视图的图标，可以看到上线主机的信息为普通用户：zhxxxx
![](https://img-blog.csdnimg.cn/20210412142036576.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)

### 4、提权
CS里面含有自动化的提权
右键选择第一个，进入命令行模式（具体命令可以查看文章最下面的指令大全）

![](https://img-blog.csdnimg.cn/20210412142307829.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)

![](https://img-blog.csdnimg.cn/20210412142403575.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)


测试执行命令：getuid，稍等一会儿后会显示执行结果

![https://img-blog.csdnimg.cn/20210412143220746.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70](https://img-blog.csdnimg.cn/20210412143220746.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)


接下来右键选择提权，如下图所示

![](https://img-blog.csdnimg.cn/20210412143333794.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)


默认提权的exp就下面这两个，肯定不够，所以得去加载一些提权的插件

**常用的插件地址：**
https://github.com/DeEpinGh0st/Erebus
https://github.com/rsmudge/ElevateKit


![](https://img-blog.csdnimg.cn/20210412143358960.png)

下载其中一个提权插件并保存，本示例下载的是：https://github.com/rsmudge/ElevateKit

![](https://img-blog.csdnimg.cn/2021041214392877.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)

**如何加载插件？**
如下图所示，选择脚本管理器后，会在下面弹窗提示path

![](https://img-blog.csdnimg.cn/20210412143618957.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)

之后选择 插件 并点击打开

![](https://img-blog.csdnimg.cn/20210412144018402.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)

之后点击 Unload 上传插件
![](https://img-blog.csdnimg.cn/20210412144149852.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)

之后再查看提权的EXP，发现增加了很多

![](https://img-blog.csdnimg.cn/202104121442428.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)

接下来利用 uac-schtasks 的 exp进行提权


![](https://img-blog.csdnimg.cn/20210412150118389.png)


点击开始之后，可以通过命令看出正在进行攻击测试了，攻击成功的话会上线一个权限为：SYSTEM 的系统，如下图所示，即是成功提权




![](https://img-blog.csdnimg.cn/20210412150225966.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDQxMjAzNw==,size_16,color_FFFFFF,t_70)




### 4.2 Cobalt Strike ——CS与MSF相互联动传递（Empire）


# ExternalC2 拓展模块

ExternalC2是Cobalt Strike引入的一种规范（或者框架），黑客可以利用这个功能拓展C2通信渠道，而不局限于默认提供的`HTTP(S)/DNS/SMB`通道。大家可以参考此处下载完整的规范说明。

简而言之，用户可以使用这个框架来开发各种组件，包括如下组件：

1、第三方控制端（`Controller`）：负责连接Cobalt Strike TeamServer，并且能够使用自定义的C2通道与目标主机上的第三方客户端（Client）通信。

2、第三方客户端（`Client`）：使用自定义C2通道与第三方Controller通信，将命令转发至 `SMB Beacon`。

3、SMB Beacon：在受害者主机上执行的标准 `beacon`。

从CS提供的官方文档中，我们可以看到如下示意图：



## 使用方式
[官方文档](https://hstechdocs.helpsystems.com/manuals/cobaltstrike/current/userguide/content/topics/listener-infrastructue_external-c2.htm?cshid=1043)

[ExternalC2
](https://github.com/ryhanson/ExternalC2)

[ExternalC2的中文翻译](https://xz.aliyun.com/t/2239)


# CobaltStrike 免费域名通过 CDN Https 上线

[CobaltStrike 免费域名通过 CDN Https 上线
](https://zeo.cool/2020/10/13/CS%E9%80%9A%E8%BF%87(CDN+%E8%AF%81%E4%B9%A6)powershell%E4%B8%8A%E7%BA%BF%E8%AF%A6%E7%BB%86%E7%89%88/)

[参考](https://blog.zjun.info/tech/cobaltstrike-goes-online-via-cdn-and-https/)

![](https://img-blog.csdnimg.cn/img_convert/3179004d6115f5f9361413a40108eed2.png)
# 参考

##  知识库

[Cobalt_Strike_wiki](https://github.com/aleenzz/Cobalt_Strike_wiki)


[转载：](https://blog.csdn.net/weixin_40412037/article/details/115552975)


