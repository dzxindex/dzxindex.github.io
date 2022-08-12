---
layout: post
title: 安装 docker 和 docker compose
categories: 工具类
description: 快速安装 docker
keywords: docker
---

## 通用安装 docker 和 docker compose

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


## kali 安装 docker

```
第一步：更新apt
$ apt-get update

第二步：安装必要组件
$ apt-get install -y apt-transport-https ca-certificates
$ apt-get install dirmngr

第三步：apt换源[清华教育] 可以选择阿里、中科大等其他源
$ curl -fsSL https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/debian/gpg | sudo apt-key add -

$ echo 'deb https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/debian/ buster stable' | sudo tee /etc/apt/sources.list.d/docker.list

第四步：安装最新版本docker 以及docker文件管理项目
$ apt-get install docker docker-compose
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




