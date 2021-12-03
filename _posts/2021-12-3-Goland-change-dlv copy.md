---
layout: post
title: Goland debug 模式更新
categories: [cate1, cate2]
description: Golang Delve版本太低无法Debug
keywords: Goland , 编辑器
---

# 问题描述
Golang无法debug原因，Golang delve 版本太低，需更新

# 解决方法

1. 直接打开cmd操作，不要在项目内
`go get github.com/go-delve/delve/cmd/dlv`


> ps:如果操作有问题，可以参看作者的文档：https://github.com/derekparker/delve/blob/master/Documentation/installation/windows/install.md

1. 找到下载的delve，默认存放的地址是：%GOROOT%/bin/delve/dlv.exe

2. 设置Goland
依次打开：Help->Edit Customer Properties；若提示文件不存在，点击创建即可

4. 在文件中新增：
```
dlv.path=你的dlv路径（windows的路径需要转义）
ps:
dlv.path=C:/Go/bin/dlv.exe
```

> ps windows路径需要转义

5. 最后重启Goland即可（刚配置好后的第一次重启会比较慢）



