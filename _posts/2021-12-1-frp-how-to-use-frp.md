---
layout: post
title: frp内网穿透
categories: [安全工具]
description: command
keywords: 安全工具
---

# 为什么需要内网穿透？


如果公司的内网不给提供外网访问，或者没有给分配外网可以访问的IP，我们又需要访问SSH登录内网的服务器，远程桌面、远程文件我们该怎么办？
远程桌面使用TeamViewer，但需要访问端也拥有TeamViewer软件，不方便。且TeamViewer不易实现远程文件访问。
使用蒲公英相关的拨号软件进行组网，可用，但免费版本网络速度极慢，体验不佳，几乎无法正常使用。
使用花生壳软件进行DNS解析，可用，但同第二点所述，免费版本有带宽限制，无法实际使用。

那么上述的场景怎么既简单又高效的实现内网穿透呢？高效的frp是一个不错的选择。



# frp的作用

1. 利用处于内网或防火墙后的机器，对外网环境提供 http 或 https 服务。
3. 对于 http, https 服务支持基于域名的虚拟主机，支持自定义域名绑定，使多个域名可以共用一个80端口。
2. 利用处于内网或防火墙后的机器，对外网环境提供 tcp 和 udp 服务，例如在家里通过 ssh 访问处于公司内网环境内的主机。

# 安装

下载：

`wget https://github.com/fatedier/frp/releases/download/v0.22.0/frp_0.22.0_linux_amd64.tar.gz`


# 服务端设置

```
# vim frps.ini

[common]
bind_port = 7000
dashboard_port = 7500
token = 12345678
dashboard_user = admin
dashboard_pwd = admin
```

- frps 服务端启动程序
- frps.ini 服务端配置文件
- frps_full.ini 服务端全量配置文件


## 运行

编辑保存完成以后，此时我们可以运行一下，执行以下命令运行。

```
./frps -c frps.ini

```


# 客户端设置


```
# vim frpc.ini
[common]
server_addr = 49.233.169.171
server_port = 7000
token = 12345678

[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 8001 # 本地监听端口

```
- server_addr就是你公网服务器的IP。
- server_port服务端设置的端口。
- token跟服务端设置的token保持一致即可。
- type为代理的类型，SSH服务设置为tcp类型。
- local_ip为本地IP。
- local_port为内网客户端设置的SSH端口。
- remote_port为内网提供给外网访问的服务端口。

## 运行

放在/app 目录下

```
/app/frp/frpc -c /app/frp/frps.ini
```

## frp后台运行
`nohup /app/frp/frpc -c /app/frp/frps.ini &`

> 进入虚拟机操作，不能通过ssh软件

# 客户端连接

**ssh -p 客户端端口 用户@IP**

```
ssh -p 本地监听端口 用户名@服务端IP
如：
ssh -p 8001 root@119.96.220.225
```


# 参考
转载：https://juejin.cn/post/6854573210306871304#heading-4