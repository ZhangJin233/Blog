---
title: "Adb命令"
date: 2019-06-18T18:23:30+08:00
draft: true
author:
  name: "Jane"
comments: true
description: ""
images:
tags:
  - adb
---

一、adb命令是什么？

adb 是安卓调试桥，用于电脑端与模拟器或真实设备交互

ADB 分为三部分:PC上的adb client 和 adb server 以及Android设备上的adb daemon(adbd)

adb 官方文档：https://developer.android.com/studio/command-line/adb.html#howadbworks

https://github.com/mzlogin/awesome-adb

常用adb命令
adb -s <seriaNum> command 指定相应的seriaNum号的设备去执行adb 命令

adb devices 获取连接状态

- device 已经连上

- offline 未连接成功或者无响应

- no device 没有设备/模拟器连接

- unauthorized 手机没有信任

adb start-server 启动 adb 服务

adb kill-server 停止 adb 服务

adb version 查看 adb 版本

adb shell 进入 adb 命令行

adb connect <device-ip> 通过 ip 地址连接设备

adb install xxx.apk 安装apk

adb install -r xxx.apk 覆盖安装apk

adb uninstall [-k] <packageName> 卸载应用，-k 保留数据和缓存

adb logcat | grep xxx 查看端上日志

adb logcat -c 清空日志

adb logcat -v time *:W 查看warning日志，并且输出时间戳

adb shell getprop 获取系统属性

adb shell getprop ro.product.model 查看设备型号

adb shell getprop ro.build.version.release 查看安卓系统版本

adb shell wm size 查看屏幕分辨率

adb shell; su; cat /data/misc/wifi/*.conf 查看连过的wifi密码

adb shell ps 查看进程

adb kill 'pid' 杀死进程

adb reboot 重启手机


aapt命令：

aapt 是Android资源打包工具



adb dump：