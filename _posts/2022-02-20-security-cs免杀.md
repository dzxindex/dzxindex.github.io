---
layout: post
title: CobaltStrike简易免杀后门制作
categories: 安全工具
description: CobaltStrike简易免杀后门制作
keywords: cs
---


## 一、相关工具地址


[微步沙箱](https://s.threatbook.cn/)

[BypassAV插件](https://github.com/hack2fun/BypassAV)

[CS安装]([./2022-02-20-security-CsInstall.md](https://dzxindex.github.io/2022/02/20/security-CsInstall/))

[FuckAV 免杀](https://github.com/iframepm/FuckAV)


## 二.后门病毒的制作

进来之后我们选择Attacks中的BypassAV(我使用的是CS4.0，没有BypassAV，所以我们可以下载bypass.cna之后通过Cobalt Strike->Script Manager来添加这个模块)

![](https://img-blog.csdnimg.cn/20210820163205885.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDc4NzgzMg==,size_16,color_FFFFFF,t_70)

然后制作一个后门(注:勾选上x64)

![https://img-blog.csdnimg.cn/20210820163206801.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDc4NzgzMg==,size_16,color_FFFFFF,t_70](https://img-blog.csdnimg.cn/20210820163206801.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDc4NzgzMg==,size_16,color_FFFFFF,t_70)


制作完成

## 三、免杀操作

使用 [FuckAV 免杀](https://github.com/iframepm/FuckAV) 免杀生成工具，加密cs生成木马

1. cs 生成木马
   attack -> paylaod generat ->  powershell

2. 使用 FuckAV 免杀


[FuckAV 免杀教程](https://github.com/iframepm/FuckAV/blob/main/upx/powershell.gif)






## 四、免杀操作-BypassAV

> 效果并不好

步骤一：在Restorator中将其他程序的属性覆盖在该后门病毒中，我这里选的是网易云

做完之后是这样子：

![](https://codeantenna.com/image/https://img-blog.csdnimg.cn/20210820163205860.png)

步骤二：使用safengine对该后门进行保护

![](https://codeantenna.com/image/https://img-blog.csdnimg.cn/20210820163206469.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDc4NzgzMg==,size_16,color_FFFFFF,t_70)


现在这个BypassAV_se就是可以免杀了



## 四.测试

进入[微步沙箱](https://s.threatbook.cn/)查杀