---
title: "使用docker 快速搭建 STF"
date: 2020-05-07T10:42:34+08:00
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

PS.如果报错:
```
docker: Error response from daemon: Mounts denied: 
The path /srv/rethinkdb
is not shared from OS X and is not known to Docker.
You can configure shared paths from Docker -> Preferences... -> File Sharing.
See https://docs.docker.com/docker-for-mac/osxfs/#namespaces for more info.
```
参考：https://stackoverflow.com/questions/45122459/docker-mounts-denied-the-paths-are-not-shared-from-os-x-and-are-not-known

 #再启动adb service
 docker run -d --name adbd --privileged -v /dev/bus/usb:/dev/bus/usb --net host sorccu/adb:latest
 #再启动stf
 docker run -d --name stf --net host openstf/stf stf local --public-ip your-ip

```

访问localhost:7100

----------------------------------
### 构建自己的STF镜像

STF docker镜像其实就是一个完整的linux系统加上stf环境和代码，因此构建镜像的过程是这样的：

1、pull一个操作系统作为base镜像，这里以ubuntu为例。

2、在ubuntu上安装stf基础环境，包括nodejs、zmq、python、git等。

3、把stf的代码塞到docker镜像中。

stf的源码中已经给出构建官方docker镜像的Dockerfile https://github.com/openstf/stf/blob/master/Dockerfile



#### 通过dockerfile创建自己的docker images

- docker pull ubuntu

- mkdir -p dockerfile/stf

- 创建Dockerfile文件

    vim dockerfile/myip/Dockerfile

- 将这个dockerfile https://github.com/openstf/stf/blob/master/Dockerfile 的内容复制到新创建的文件中

- 构建镜像

    cd dockerfile/stf/

- docker build -t stf-local .

## or第二种方法（第一种dockerfile 创建本地镜像的方法没有成功，使用下面👇这种成功了）

1、Cloned the STF repo

2、cd stf/

3、docker built -t stf-local . and then everything ran fine :)