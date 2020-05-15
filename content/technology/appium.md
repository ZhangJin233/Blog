---
title: "mac 安装Appium环境 及 iOS真机启动"
date: 2020-05-14T14:04:42+08:00
draft: true
author:
  name: "阿金"
comments: true
description: "appium iOS Android"
keywords: ["appium","ios","android"]
images:
tags:
  - test
---

-----------------准备工作-------------------

1、下载Android studio

2、下载xcode

3、下载appium destop

4、安装homebrew、carthage、node、npm

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

brew install libimobiledevice --HEAD

brew install carthage

brew install node

brew install npm

npm install -g ios-deploy

gem install xcpretty

npm install -g appium

npm install -g appium-doctor

```

5、使用appium-doctor检查appium环境

