---
layout: post
title: prometheus 钉钉告警 
categories: [prometheus]
description: prometheus-webhook-dingtalk
keywords: prometheus 
---

# prometheus-webhook-dingtalk



## docker 部署 prometheus-webhook-dingtalk


1. 钉钉 token 如下：
   
```
https://oapi.dingtalk.com/robot/send?access_token=XXXXXX

```

1. 执行 docker 安装 prometheus-webhook-dingtalk 

```
docker run -d --restart always -p 8060:8060 timonwong/prometheus-webhook-dingtalk:v0.3.0 --ding.profile="webhook-test=https://oapi.dingtalk.com/robot/send?access_token=XXXXXX"
```
> 添加钉钉token


3.查看prometheus-webhook-dingtalk容器运行情况

```
root@test03:/usr/local/alertmanager# docker ps|grep prometheus-webhook-dingtalk
34dcac5e1baf        timonwong/prometheus-webhook-dingtalk:v0.3.0   "/bin/prometheus-web…"   16 hours ago        Up 16 hours         0.0.0.0:8060->8060/tcp   clever_varahamihira
```

4. 下载项目,测试发送

```
git clone https://github.com/timonwong/prometheus-webhook-dingtalk.git
cd prometheus-webhook-dingtalk
sh examples/send_alerts.sh
```

> 修改 send_alerts.sh 发送路径

5. 钉钉收到信息


## 参考

[prometheus-alertmanager-webhook-for-dingtalk](https://theo.im/blog/2017/10/16/release-prometheus-alertmanager-webhook-for-dingtalk/)


