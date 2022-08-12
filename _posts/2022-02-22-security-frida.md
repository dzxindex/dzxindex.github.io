---
layout: post
title: frida 入门及几种 hook 思路
categories: [安全工具]
description:  frida是个全能Hook框架
keywords:  frida
---

## 0x01 简介

frida 是一款基于 python+javascript 的 hook 框架，可运行在 android、ios、linux、win等各个平台，主要使用的动态二进制插桩技术。


## 0x02 插桩技术
是指将额外的代码注入程序中以收集运行时的信息，可分为源代码插桩 SCI 和二进制插桩 BI。

源代码插桩 SCI

Source Code Instrumentation，额外代码注入到程序源代码中。

二进制插桩 BI

- Binary Instrumentation，额外代码注入到二进制可执行文件中。

- 静态二进制插桩 SBI，Static Binary Instrumentation，在程序执行前插入额外的代码和数据，生成一个永久改变的可执行文件。

- 动态二进制插桩 DBI
，Dynamic Binary Instrumentation，在程序运行时实时插入额外代码和数据，对可执行文件没有任何永久改变。


## 0x03 Frida安装

[官方地址](https://frida.re/)
[github地址](https://github.com/frida/frida)


- PC 端
  
    python 安装

    编译安装

- Android 端
  
    已 root 设备

    非 root 设备

### 一、PC端

安装 frida CLI(command-line interface，命令行界面)

**python 安装**

```
pip3 install frida

```
pip 安装 frida CLI，pip install frida，过程遇到Running setup.py bdist_wheel for frida ...\较慢，请耐心等候

**源码编译安装**

```
git clone git://github.com/frida/frida.git
cd frida
make
```
> 注意安装版本，系列工具版本号要一致

查看 frida 版本号

```
frida --version 
12.2.27
```

> frida 共有6个工具：firda CLI，frida-ps，frida-trace，frida-discover，frida-ls-devices，frida-kill

### 二、Android 端

电脑 USB 连接安卓手机，针对设备是否 root 采用不同的方式


1. 已 root 设备

已经 root 的设备采用安装 frida-server 的方式

1. 查看手机型号，下载系统对应版本的 [frida-server](https://github.com/frida/frida/releases)

```
adb shell getprop ro.product.cpu.abi
```
例如型号为 **arm64-v8a**，则下载 [frida-server-12.2.27-android-arm64.xz](https://github.com/frida/frida/releases/download/12.2.27/frida-server-12.2.27-android-arm64.xz)

2. 将其解压缩生成 frida-server-12.2.27-android-arm64 文件


3. 将解压之后的文件push 到设备中，指定到 /data/local/tmp 路径下重命名为 frida-server

```
adb push frida-server-12.2.27-android-arm64 /data/local/tmp/frida-server
```

4. 运行Android 设备中的 frida-server


```
adb shell
su
cd /data/local/tmp
chmod 755 frida-server
./frida-server
```

执行完毕后为运行状态。

保留此窗口 shell，以保证服务运行，关闭该shell 或者停止ctrl+c 则服务关闭。接下来的操作可另起shell 或该步骤命令另起 shell 执行。

5. 进行端口转发监听

```
adb forward tcp:27042 tcp:27042
adb forward tcp:27043 tcp:27043
```

27042 用于与frida-server通信的默认端口号,之后的每个端口对应每个注入的进程，检查27042端口可检测 Frida 是否存在。

6. 检查是否成功

执行 `frida-ps -U` 命令成功输出进程列表，如下所示

```
$> frida-ps -U
PID  Name
-----  ----------------------------------------
 4275  com.android.keyguard
 4629  com.android.phone
 5182  com.android.contacts:cacheservice
 ...
```


执行 `frida -U -f com.xxx.xxx` 进行连接，选择一个进程，等待一段时间则进入该应用

```
$> frida -U -f com.xxx.xx
     ____
    / _  |   Frida 12.2.27 - A world-class dynamic instrumentation toolkit
   | (_| |
    > _  |   Commands:
   /_/ |_|       help      -> Displays the help system
   . . . .       object?   -> Display information about 'object'
   . . . .       exit/quit -> Exit
   . . . .
   . . . .   More info at http://www.frida.re/docs/home/
Spawned `com.xxx.xxx`. Use %resume to let the main thread start executing!
```

### 2. 非 root 设备

没有 root 的设备采用安装 frida-gadget 的方式，需要对目标应用 apk 进行反编译注入和调用

手动注入frida-gadget


# 参考

转载：https://www.jianshu.com/p/bab4f4714d98

