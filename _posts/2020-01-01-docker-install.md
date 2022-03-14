---
layout: post
title: 安装 docker 和 docker compose
categories: 工具类
description: 快速安装 docker
keywords: docker
---
## nodejson格式

## 安装 docker 和 docker compose

```shell
# docker
curl -sSL https://get.daocloud.io/docker | sh

# docker compose
curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
# 国内用户可以使用以下方式加快下载
curl -L https://download.fastgit.org/docker/compose/releases/download/1.27.4/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose

chmod +x /usr/local/bin/docker-compose
ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
docker-compose --version


```




##  docker 换源

```

mkdir /etc/docker/
cat > /etc/docker/daemon.json <<EOF
{
"registry-mirrors": [
"https://registry.docker-cn.com",
"http://hub-mirror.c.163.com"
],
"dns": ["8.8.8.8","8.8.4.4"]
}
EOF


最后重启docker

service docker restart
systemctl enable docker
```




