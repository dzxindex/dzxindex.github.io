---
layout: post
title: docker command
categories: [docker]
description: command
keywords: docker, keyword2
---

# delete 

```shell

# 删除全部镜像
docker rmi $(docker images -q)

# 停止所有容器
docker stop $(docker ps -aq)

```
