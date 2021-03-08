---
title: "EarlGrey2 cocoapods 安装 及 使用 "
date: 2020-11-27T11:06:20+08:00
author:
  name: "阿金"
comments: true
description: "EarlGrey2 UI test"
keywords: ["EarlGrey2","objective-c"]
images:
tags:
  - EarlGrey2
  - IOS UI test
---

一、EarlGrey2 cocoapods 安装

1、在podfile 引入 EarlGrey2依赖，不用具体到EarlGrey2 branch

``` ruby
target 'EarlGreyExampleSwift' do
  pod 'EarlGreyApp'
end

target 'EarlGreyExampleUITests' do
  #inherit! :search_paths
  pod 'EarlGreyTest'
end

target 'EarlGreyExampleSwiftUITests' do
  #inherit! :search_paths
  pod 'EarlGreyTest'
end

```

2、pod install 下载相应文件依赖

3、运行的时候，如果报错  bitcode bundle could not be generated because ...

在pods 文件下 找到 TARGETS的 EarlGreyTest ，将 enable Bitcode 设置为NO

{{<figure src="/images/EarlGrey2.png" alt="EarlGrey2">}}

4、运行项目，运行成功

二、EarlGrey2 原理及使用


EarlGrey 2.0 is a native iOS UI automation test framework that combines EarlGrey with XCUITest, Apple's official UI Testing Framework.

EarlGrey 2.0 allows you to write clear, concise tests in Objective-C / Swift and enables out of process interactions with XCUITest. It has the following chief advantages:

Synchronization: From run to run, EarlGrey 2.0 ensures that you will get the same result in your tests, by making sure that the application is idle. It does so by automatically tracking UI changes, network requests and various queues. EarlGrey 2.0 also allows you to manually implement custom timings.

White-box: EarlGrey 2.0 allows you to query the application under test from your tests.

Native Development: As with EarlGrey 1.0, you can use EarlGrey 2.0 natively with Xcode. You can run tests directly from Xcode or xcodebuild. Please note that EarlGrey 2.0 uses a UI Testing Target and not a Unit Testing Target like EarlGrey 1.0.

EarlGrey 1.0 is a white-box testing tool that allows you to interact with the application under test. Since XCUITest is a black-box testing framework, this is not directly possible with EarlGrey 2.0. To fix this, we use eDistantObject (eDO) to allow these white-box interactions.

这是官方GitHub给的说明，主要就是几点：

- EarlGrey 2.0 是基于原生的Apple UI 测试框架 XCUITest

- EarlGrey 2.0 可以支持 Objective-C / Swift，可以直接在Xcode的中运行使用

- EarlGrey 2.0 不可以在Unit Testing 中使用（EarlGrey 1.0是可以的）

- eDistantObject (eDO) 是为了 使EarlGrey 2.0 支持 白盒测试

- EarlGrey 2.0 可以测试 UI 变化，网络请求以及各种问题


#### EarlGrey 2.0 advantages over XCUITest
- Automatic synchronization with Animations, Dispatch Queues, and Network Requests as enumerated here.

- In-built White-Box Testing Support with RMI.

- Better Support for Flakiness（分层） Issues.

- Better Control of tests. EarlGrey has a much larger set of matchers.

- EarlGrey performs a pixel-by-pixel（逐个像素） check for the visibility of an element.

#### EarlGrey 2.0 advantages over EarlGrey 1.0
- Out of Process Testing using XCUITest. So System Alerts, Inter-app interactions etc. are supported

- Lesser throttling of the application under test's main thread.

- Better support since accessibility is provided out of the box with XCUITest.


可以参考官方文档以及 demo：

https://github.com/google/EarlGrey/blob/earlgrey2/Tests/Functional/Sources/SystemAlertHandlingTest_IOS13OrLater.m

http://google.github.io/EarlGrey/index.html

https://github.com/google/EarlGrey/blob/earlgrey2/Demo/EarlGreyExample/EarlGreyExampleUITests/EarlGreyExampleUITests.m



三、Tapping system alert using EarlGrey 2.0 & Swift or objective-c

##### objective-c

``` swift

- (void) testButterAlerts{
    //Notifications
    XCTAssertTrue([EarlGrey selectElementWithMatcher:grey_systemAlertViewShown()]);
    XCTAssertTrue([EarlGrey selectElementWithMatcher:grey_buttonTitle(@"“APP”想给您发送通知")]);
    XCTAssertTrue([self grey_waitForAlertVisibility:YES withTimeout:1]);
    XCTAssertTrue([self grey_acceptSystemDialogWithError:nil]);
    XCTAssertTrue([self grey_waitForAlertVisibility:NO withTimeout:1]); 
}

```

##### swift


``` swift

func testExample() {
    let app = XCUIApplication()
    app.launch()
    XCTAssertTrue(grey_wait(forAlertVisibility: true, withTimeout: 2))
    XCTAssertTrue(grey_acceptSystemDialogWithError(nil))
    XCTAssertTrue(grey_wait(forAlertVisibility: false, withTimeout: 1))    
}
```