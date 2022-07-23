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

### 一、支付流程

1. APP向服务器发送请求，获得一份产品列表
2. 服务器返回包含产品标识符的列表
3. APP向App Store发送请求，得到产品的信息
4. App Store返回产品信息
5. APP把返回的产品信息显示给用户（App的store界面）
6. 用户选择某个产品
7. APP向App Store发送支付请求
8. App Store处理支付请求并返回交易完成信息
9. APP从信息中获得数据，并发送至服务器
10. 服务器记录数据，并进行审查
11. 服务器将数据发给App Store来验证该交易的有效性
12. App Store对收到的数据进行解析，返回该数据和说明其是否有效的标识
13. 服务器读取返回的数据，确定用户购买的内容
14. 服务器将购买的内容传递给程序

### 二、IAP(In‑App Purchase) 支付：
#### StoreKit 相关字段的信息：

```Obj-c
/// The unique product identifier.
public let id: String

/// The type of the product.
public let type: Product.ProductType

public let subscription: Product.SubscriptionInfo?

public subscript(key: Product.Key) -> BackingValue { get }
```
- id 是指商品在苹果记载的ID


- ProductType是商品的类型
 四种订阅类型，这里每种类型就简单举个：

  - consumable （消耗型商品），可以反复购买，购买后的商品会被一次性消费。
  - nonConsumable （非消耗型商品），游戏解锁新关卡就是这个类型，只能买一次，买了之后永久有效。
  - autoRenewable （自动续期订阅），每个周期会自动扣款的商品，例如 会员续费。
  - nonRenewable （非自动续期订阅 ），不会自动扣款的，可多次订阅的商品。

```Obj-c
public struct ProductType {

    public static var consumable: Product.ProductType

    public static var nonConsumable: Product.ProductType

    public static var nonRenewable: Product.ProductType

    public static var autoRenewable: Product.ProductType
}
```
- Subscription info 只有 .autoRenewable 类型的商品才会有这个属性
在Subscription info中有一个属性： isEligibleForIntroOffer，这个是现在用的比较多的首次购买优惠。
例如一些 APP 会有会员订阅服务，那些服务会有 1 个月，3 个月，12 个月等的自动续期，同时还会有一些第一次购买的优惠，这个第一次购买的优惠就是首购优惠，并且这个优惠跟 Apple ID 挂钩，跟 APP 内自己的账号体系无关。

```Obj-c

/// Whether the user is eligible to have an introductory offer applied to their purchase.
public var isEligibleForIntroOffer: Bool { get async }

/// Whether the user is eligible to have an introductory offer applied to a purchase in this
/// subscription group.
/// - Parameter groupID: The group identifier to check eligibility for.
public static func isEligibleForIntroOffer(for groupID: String) async -> Bool

```

#### 用 StoreKit 发起购买
- Request
Request 方法就能获取到上一章说的 Product 类型。传入需要的 ProductId 就能返回对应的信息。

通过 Product.request 去请求你需要的 Product 类型数据，然后根据订阅类型存到不同的数组中。

- Purchase

- Payment

{{< image src="/images/IAP.png" alt="IAP" position="center" style="border-radius: 8px;" >}}

### 三、测试准备：
1、准备沙盒账户
登录苹果开发者后台--App Store Connect--用户和访问--沙盒--测试员--添加，可以选择相应的地区，如果不涉及海外用户一般选择中国地区。

iOS15以及以上的系统，可以管理沙盒购买的订阅，这个对于测试订阅比较方便。

2、证书

dev证书和adhoc证书的包为测试包，只能用沙盒账号进行支付，线上包是不能沙盒支付的。

iOS证书主要分：

  - dev dev的包主要用于前期测试，使用的是开发证书
  - App Store  App Store的包是上传至App Store时需要选择的
  - Enterprise  证书为企业签，任何一台手机都可以安装了
  - adhoc 个人签，打包时也需要加入udid才能安装
 

### 四、测试要点：
- 显示的货币与价格，符合预期，如果产品app在多个国家上线还应该查看各个国家的价格是否正确
- 支付流程能正常完成，商品也成功到账
- 支付完成后是否正常刷新界面
- 在购买交易中，通过付款方式扣款失败，用户不应收到商品。
- 可以多次购买的商品确保商品可以多次购买

由于涉及到续订、退订、体验期、首次折扣价格等操作，订阅的测试相对来说更复杂一些，QA侧需要额外关注以下几点：

- 需要验证所有的价格显示、支付流程、到账流程、涉及金额或权限的变化等通用case

根据游戏内订阅商品的实际配置，如是否有免费试用、是否有首次购买折扣等，参考官方用例，完成游戏自己的测试用例。

- 续订功能正常，一般沙盒账户可以设置续订周期，20分钟一次自动续订
- 退订后不再扣款，并且相应的会员权益在截止日期后特权不生效
- 如果有首次优惠，已经使用首次购买的用户和没有首次购买的用户看到的价格不同
- 首次购买完成后，价格应该显示正常价格
- 体验期内不扣款
- 体验期内退订
- 已经订阅的用户再次购买订阅
- 切换Apple ID进行购买
- 切换app账户购买，具体要看产品的逻辑，购买时Apple ID和app ID是否绑定
- 用户发起退款，这个需要在线上测试
- 黑产利用Apple 的退款机制，退款后大部分游戏内的点券并不会随着退款而消失，造成损失。

4、testflight支付

 使用testflight的用户在支付的时候，是使用沙盒支付，即使是正常用户也是沙盒支付。所以需要规避这个问题。

### 五、其他方式保证支付功能

iOS应用内的第三方支付：

- 微信
- 支付宝
- PayPal

如果app内有第三方支付，提交审核的时候很可能被拒，最好关掉
