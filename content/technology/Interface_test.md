---
title: "API测试"
date: 2019-11-13T11:29:26+08:00
draft: true
author:
  name: "Jane"
comments: true
description: ""
keywords:
images:
tags:
  - test
---
一、什么是API测试？

API测试的基本步骤如下：

（1）、准备测试数据

（2）、通过API测试工具发起对被测API的请求

（3）、验证相应

二、API测试工具

1、命令行工具cURL
- 基本用法
首先下载安装cURL。然后通过命令发起对API的调用

```bash
$ curl https://www.google.com
```
上面命令向www.google.com发出get请求，服务器返回的内容会在命令行输出。

**-A**
-A参数指定客户端的user-Agent。curl的默认用户代理字符串是：curl/[version]




2、图形界面工具Postman、SoapUI

3、API性能测试工具JMeter

三、API测试实践


