---
layout: post
title: GO 语言的 socket 通讯
categories: [ socket , GO ]
description: socket 通讯方式
keywords: socket , GO
---


# socket 通讯方式


## Go 语言使用 net 包实现 Socket 网络编程

###  server 端

```
package main

import (
    "bufio"
    "fmt"
    "net"
)

func process(conn net.Conn) {
    // 处理完关闭连接
    defer conn.Close()

    // 针对当前连接做发送和接受操作
    for {
        reader := bufio.NewReader(conn)
        var buf [128]byte
        n, err := reader.Read(buf[:])
        if err != nil {
            fmt.Printf("read from conn failed, err:%v\n", err)
            break
        }

        recv := string(buf[:n])
        fmt.Printf("收到的数据：%v\n", recv)

        // 将接受到的数据返回给客户端
        _, err = conn.Write([]byte("ok"))
        if err != nil {
            fmt.Printf("write from conn failed, err:%v\n", err)
            break
        }
    }
}

func main() {
    // 建立 tcp 服务
    listen, err := net.Listen("tcp", "127.0.0.1:9090")
    if err != nil {
        fmt.Printf("listen failed, err:%v\n", err)
        return
    }

    for {
        // 等待客户端建立连接
        conn, err := listen.Accept()
        if err != nil {
            fmt.Printf("accept failed, err:%v\n", err)
            continue
        }
        // 启动一个单独的 goroutine 去处理连接
        go process(conn)
    }
}
```

### client 端

```
package main

import (
    "bufio"
    "fmt"
    "net"
    "os"
    "strings"
)

func main() {
    // 1、与服务端建立连接
    conn, err := net.Dial("tcp", "127.0.0.1:9090")
    if err != nil {
        fmt.Printf("conn server failed, err:%v\n", err)
        return
    }
    // 2、使用 conn 连接进行数据的发送和接收
    input := bufio.NewReader(os.Stdin)
    for {
        s, _ := input.ReadString('\n')
        s = strings.TrimSpace(s)
        if strings.ToUpper(s) == "Q" {
            return
        }

        _, err = conn.Write([]byte(s))
        if err != nil {
            fmt.Printf("send failed, err:%v\n", err)
            return
        }
        // 从服务端接收回复消息
        var buf [1024]byte
        n, err := conn.Read(buf[:])
        if err != nil {
            fmt.Printf("read failed:%v\n", err)
            return
        }
        fmt.Printf("收到服务端回复:%v\n", string(buf[:n]))
    }
}
```


## server 如何进行 push 操作？

### golang中怎么处理socket长连接？

我是golang新手，看了下goroutine+channel，我认为很适合服务器端并发编程。
我在网上看到的demo都是千篇一律的accept到一个client fd后，开一个goroutine处理client fd。是一问一答式的，client发来一个请求，server回应，都是在一个goroutine里面处理的。

但是服务器应该是可以主动push message的。我想的事为每个client fd开两个goroutine，一个recv，一个send。同时还有加2个channel，一个用于recv routine向逻辑主线程传送收到的数据，一个用于逻辑主线程向send goroutine传送待发送的数据，是这样的么？

还有，如果我开2个goroutine的话，client断开连接了，假设recv goroutine先发生err并且close(fd)，那在send goroutine中该如何处理呢？有可能不应该这样处理，那应该怎么处理呢？

####  socket长连接解决方案

使用 cellnet 模块

链接地址：[cellnet](https://github.com/davyxu/cellnet))

## 参考

https://segmentfault.com/a/1190000022734659
https://github.com/davyxu/cellnet
https://www.liwenzhou.com/posts/Go/15_socket/