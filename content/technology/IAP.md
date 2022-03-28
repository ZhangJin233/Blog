---
title: "IAP支付测试"
date: 2022-03-28T14:21:23+08:00
draft: true
author:
  name: "Jane"
comments: true
description: "支付"
keywords:
images:
tags:
  - 支付
---

一、支付流程

1. APP向服务器发送请求，获得一份产品列表
2. 服务器返回包含产品标识符的列表
3. APP向App Store发送请求，得到产品的信息
4. App Store返回产品信息
5. APP把返回的产品信息显示给用户（App的store界面）
6. 用户选择某个产品
7. APP向App Store发送支付请求
8. App Store处理支付请求并返回交易完成信息
9. APP从信息中获得数据，并发送至服务器
10. 服务器纪录数据，并进行审(我们的)查
11. 服务器将数据发给App Store来验证该交易的有效性
12. App Store对收到的数据进行解析，返回该数据和说明其是否有效的标识
13. 服务器读取返回的数据，确定用户购买的内容
14. 服务器将购买的内容传递给程序

二、测试注意的点：

 - App 支付

 - App 订阅

 - 沙盒支付

 - testflight支付

三、其他方式保证支付功能
