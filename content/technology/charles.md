---
title: "Charles"
date: 2020-02-19T14:18:03+08:00
author:
  name: "Jane"
comments: true
description: "Charles rewrite  Remote Breakpoints  Throttle Settings 重写 抓包 弱网 "
keywords:
images:
tags:
  - Charles
---
工作中，抓包是常用的分析问题的手段。Mac 下Charles则是最常用的代理工具。

Charles的主要功能包括：

- 代理功能
  - HTTP/HTTPS
  - 限速模拟
  - 断点调试
- 转发
 - 映射
 - 重写
- repeat

### 1、rewrite HTTPS traffic for mobile applications ###

Mac 安装Charles 后，如果需要对移动端进行抓包，那么需要手机浏览器输入：chls.pro/ssl安装证书,然后再在WiFi连接处设置代理。（保证Charles和移动端处于同一局域网）

{{< image src="/images/charles1.png" alt="Charles" position="center" style="border-radius: 8px;" >}}



首先 Tools -》Rewrite

勾选enable rewrite

点击add，如图所示：

{{< image src="/images/charles2.png" alt="Charles2" position="center" style="border-radius: 8px;" >}}


弹出【Edit Location】 分别填入需要被mock的url（提前设置该URL enable SSL )，点击ok

{{< image src="/images/charles3.png" alt="Charles3" position="center" style="border-radius: 8px;" >}}


在右下的栏内，点击add，弹出如图的提示框，填入Rewrite Rule ，这里将百度网页的【百度一下】button 文字改为【阿金】，最后点击apply

{{< image src="/images/charles4.png" alt="Charles4" position="center" style="border-radius: 8px;" >}}

访问www.baidu.com 

{{< image src="/images/charles5.png" alt="Charles5" position="center" style="border-radius: 8px;" >}}

Rewrite 功能，不仅可以对 Response 进行修改，还可以对 Request 进行修改，只是较为常用的就是对 Response 进行修改。

### 2、Map Remote ###

Tools -》Map Remote

勾选【Enable Map Remote】

点击add
{{< image src="/images/charles6.png" alt="Charles6" position="center" style="border-radius: 8px;" >}}


填写需要 mapping 的url 以及 mapping的目的地

{{< image src="/images/charles7.png" alt="Charles7" position="center" style="border-radius: 8px;" >}}

在移动端请求www.baidu.com ,可以看到跳转知乎网页

{{< image src="/images/charles8.png" alt="Charles8" position="center" style="border-radius: 8px;" >}}


### 3、Rewriting traffic with Breakpoints ###

首先在Charles中获得需要Rewrite的url：cn.bing.com

右键点击该url 选择 Breakpoints

{{< image src="/images/charles9.png" alt="Charles9" position="center" style="border-radius: 8px;" >}}

在 Proxy->Breakpoint Settings 中勾选 Enable Breakpoints,然后双击请求弹出 Edit Breakpoint 框，选中 Response 后 OK 

{{< image src="/images/charles10.png" alt="Charles10" position="center" style="border-radius: 8px;" >}}

移动端请求cn.bing.com，这时候Charles 会跳转如下界面，并且客户端请求处于等待加载状态

点击【Edit Breakpoint】 将HTML中的【直搜全球英文信息】 改为 【Google】

然后点击【Execute】

{{< image src="/images/charles11.png" alt="Charles11" position="center" style="border-radius: 8px;" >}}

这时候cn.bing.com 网页 加载完成，界面中的【直搜全球英文信息】 显示为 【Google】

{{< image src="/images/charles11.png" alt="Charles11" position="center" style="border-radius: 8px;" >}}

### 4、Throttle Settings ###

菜单栏 proxy -》Throttle Settings

可以看到一些关于弱网模式的设置

点击 【Add】 添加需要限制网速的url，最后点击OK即可

{{< image src="/images/charles12.png" alt="Charles12" position="center" style="border-radius: 8px;" >}}


<!--adsense-->

