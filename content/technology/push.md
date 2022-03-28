---
title: "推送测试"
date: 2022-03-28T14:23:07+08:00
draft: true
author:
  name: "Jane"
comments: true
description: ""
keywords:
images:
tags:
  - untagged
---

一、开发iOS系统中的Push推送，通常有以下4种情况：

1）在线Push：比如QQ、微信等IM界面处于前台时，聊天消息和指令都会通过IM自建的网络长连接通道推送过来，这种Push在本文中暂且称为“在线Push”；

2）本地Push：这种就是最常见的iOS系统通知（作用相当于传统PC端的提示窗口，在iOS10以后全部整合到UserNotifications.framework框架了），不涉及任何网络数据，仅仅是让APP拥有一个统一系统通知方式而已，比如：闹钟的定时提醒等；

3）离线/远程Push：当APP在离线（kill掉进程、切到后台、锁屏）时，收到的消息提醒，称为离线push。离线push是需要经过苹果的APNs服务器才可以推送到某台设备的某个APP上的，这是和本地push的本质区别。push与设置中是否打开“通知”有关。离线push依赖于APNs，它使得APP处于后台或者被kill的情况下仍能收到网络通知，我们日常收到的推送消息大部分是这种。除了标题、内容、提示音和角标数字等固定推送参数以外，开发者还可以在推送消息中增加自定义参数，让用户在点击推送消息时能够直达相关新闻、邮件或福利页面，提供更好的用户体验和页面的曝光率。

4）一种特殊的远程push：静默push

严格来说，静默push属于远程push的一种特殊情况，静默push用的场景较少。

离线（远程）push与静默push的区别：

普通离线（远程）push：收到推送后（有文字有声音），点开通知，进入APP后，才执行；
静默push：收到推送（没有文字没有声音），不用点开通知，不用打开APP，就能执行，用户完全感觉不到。
所以静默push又被我们称做 Background Remote Notification（后台远程推送）。静默推送是在iOS7之后推出的一种推送方式。它与其他推送的区别在于允许应用收到通知后在后台（background）状态下运行一段代码，可用于从服务器获取内容更新。

二、什么是APNs？

APNs：Apple Push Notification service(苹果推送通知服务)

APNs主要用于以下场景：当用户主动杀掉 APP，或者 APP 进入后台超过约定时长时，APP会被kill，这样保障了前台 APP 的流畅性，也延长了手机的使用时长，获得了较好的用户体验，但是这也意味着，服务器无法主动和用户交互（如推送实时消息等），所以苹果推出了 APNs，允许设备和服务器分别与苹果的推送通知服务器保持长连接状态。

关于APNs的更新有以下几点：

  - iOS 8以后，APNs推送的字节是2k，iOS8以前是256字节；

  - iOS 9以后APNs支持HTTP/2协议栈，优化长连接，具有标准的HTTP返回和管道复用技术；

  - iOS 10以后，推送的字节是4k，APNs可根据推送消息的唯一标示符查询某条消息是否被用户阅读，可更新某一推送消息，而不用发重读的多条消息。



三、iOS推送流程

<img src="/images/push.png" height="400px" width="600px">


iOS 客户端远程消息推送的实现可以分为以下几个流程：

    - 用户的 iphone 通过 iOS 的系统方法调用与苹果的 APNs 服务器通信，获取设备的 deviceToken，它是由 APNs 服务分配的用于唯一标识不同设备上的不同 App，可以认为是由 deviceID、bundleId 和安装时的相关信息生成的，App 的升级操作 deviceToken 不变，卸载重装 App、恢复和重装操作系统后的 deviceToken 会发生变化。

    - 苹果的 APNs 服务是基于 deviceToken 实现的，因此需要将设备的 deviceToken 发送到我们的业务服务器中，用于后续的消息推送。一个设备可能登录过多个用户，一个用户也可能在多个设备中登录过，当我们需要给不同用户推送不同的消息时，除了 deviceToken 之外，我们还需要保存用户的 openid 与 deviceToken 的映射关系。我们可以在用户登录成功后的时机更新 openid 和 deviceToken 的映射关系，用户退出后取消映射关系，只保存用户最后登录设备的 deviceToken，避免一个设备收到多个重复通知和一个用户在不同设备收到多个通知等情况。

    - 在新闻类 App 出现事实热点新闻时，后台服务就可以携带消息内容和 deviceToken 等内容，向苹果的 APNs 服务发起消息推送请求，推送消息的实现是异步的，只要请求格式和 deviceToken 检查通过 APNs 服务就不会报错，但是用户还是可能因为网络异常或者关闭了推送权限等原因收不到推送消息。

    - APNs 服务向用户设备推送消息这一步也是异步的，在用户关机或网络异常收不到推送的情况下，APNs 会为每个 deviceToken 保留最后一条推送消息，待网络恢复后再次推送。



四、iOS推送要点测试：

测试要点	详情
push到达	push及时到达，并显示正常
点击push响应	点击push后跳转相应的界面
不同界面打开push	在不同界面打开push，再返回可能出现问题
系统兼容	iOS push机制不断更新，每个系统可能不一样
展开界面功能是否正常	push展开后，点击一些功能是否正常
重装app	重装后是否会收到多条异常推送
切换账户	切换账户后，是否会收到旧账户的异常推送；或切换账户后点击旧账户的推送，是否正常
角标计数	收到push后，角标+1
角标消失	点击推送或打开app后，角标消失
多端同时在线	支持多端登陆的app，是否每个客户端都能收到推送
游客状态与登陆状态	游客状态的时候，是否正常收到push，登陆账号后，是否可以收到推送

五、push调试工具

Knuff离线push工具下载链接：https://github.com/KnuffApp/Knuff/releases

SmartPush：https://github.com/shaojiankui/SmartPush
