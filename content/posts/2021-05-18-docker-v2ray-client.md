---
layout: post
title: Docker 部署 V2Ray 客户端
date: 2021-05-18 02:14:00 +08:00
category: 
author: Penguint
tags: [docker, WSL, WSL2, v2ray]
summary: 
excerpt_separator: <!-- more -->
---
<!-- more -->

# 环境

[ArchWSL](https://git.io/archwsl)

# 方案

先拉取 `v2ray` 镜像

```bash
$ docker pull v2fly/v2fly-core
```

配置文件 `jp.json`

可由图形客户端导出，加以修改 `inbounds`

```json
// 注意 listen 需为 0.0.0.0
// socks 和 http 入站协议分别提供 socks 和 http 代理服务
"inbounds": [
  {
    "tag": "socks_proxy",
    "port": 30808,
    "listen": "0.0.0.0",
    "protocol": "socks",
    "sniffing": {
      "enabled": true,
      "destOverride": [
        "http",
        "tls"
      ]
    },
    "settings": {
      "auth": "noauth",
      "udp": true,
      "ip": null,
      "address": null,
      "clients": null
    },
    "streamSettings": null
  },
  {
    "tag": "http_proxy",
    "port": 30809,
    "listen": "0.0.0.0",
    "protocol": "http",
    "sniffing": {
      "enabled": false,
      "destOverride": [
        "http",
        "tls"
      ]
    },
    "settings": {
      "timeout": 0,
      "accounts": null,
      "allowTransparent": false,
      "userLevel": 0
    }
  }
]
```

运行镜像

```bash
# 最后的 v2ray -config=/etc/v2ray/config.json 不输也行，容器内会自动运行这句
$ sudo docker run -d --name v2ray -v /etc/v2ray/jp.json:/etc/v2ray/config.json -p 30808:30808 -p 30809:30809 v2fly/v2fly-core  v2ray -config=/etc/v2ray/config.json
```

修改环境变量，配置各软件代理后就可以使用了

下次直接启动容器即可

```bash
# 启动
$ docker start v2ray

# 停止
$ docker stop v2ray

# 重启
$ docker restart v2ray
```
