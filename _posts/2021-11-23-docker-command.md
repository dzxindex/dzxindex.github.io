---
layout: post
title: docker command
categories: [docker]
description: 常用 docker command
keywords: command
---

# delete 

```shell

# 删除全部镜像
docker rmi $(docker images -q)

# 停止所有容器
docker stop $(docker ps -aq)

```
