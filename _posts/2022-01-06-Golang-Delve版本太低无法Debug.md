---
layout: post
title: Goland debug 模式更新
categories: [编辑器]
description: Golang Delve版本太低无法Debug
keywords: Goland , 编辑器
---

# Golang无法debug原因

1. goland 软件版本问题，换成2022版本
2. Golang delve 版本太低，需更新



   
直接打开cmd操作，不要在项目内

如果操作有问题，可以参看作者的文档：https://github.com/derekparker/delve/blob/master/Documentation/installation/windows/install.md

> ps: 我没有解决此问题(#`O′)，最后更换goland 2021 成功debug