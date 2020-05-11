---
title: "使用docker 快速搭建 STF"
date: 2020-05-07T10:42:34+08:00
draft: true
author:
  name: "阿金"
comments: true
description: "使用docker 快速搭建 STF"
keywords: ["docker","STF"]
images:
tags:
  - STF
---
#### docker运行SFT
1、 pull 相关镜像

首先 在docker 上 pull 这几个镜像：

docker pull openstf/stf:latest

docker pull sorccu/adb:latest

docker pull rethinkdb:latest

docker pull openstf/ambassador:latest

docker pull nginx:latest

2、启动
```shell
#先启动一个数据库
 docker run -d --name rethinkdb -v /srv/rethinkdb:/data --net host rethinkdb rethinkdb --bind all --cache-size 8192 --http-port 8090
 #再启动adb service
 docker run -d --name adbd --privileged -v /dev/bus/usb:/dev/bus/usb --net host sorccu/adb:latest
 #再启动stf
 docker run -d --name stf --net host openstf/stf stf local --public-ip your-ip

```

访问7100端口

#### 构建自己的镜像

STF docker镜像其实就是一个完整的linux系统加上stf环境和代码，因此构建镜像的过程是这样的：

1、pull一个操作系统作为base镜像，这里以ubuntu为例。
2、在ubuntu上安装stf基础环境，包括nodejs、zmq、python、git等。
3、把stf的代码塞到docker镜像中。

stf的源码中已经给出构建官方docker镜像的Dockerfile https://github.com/openstf/stf/blob/master/Dockerfile

