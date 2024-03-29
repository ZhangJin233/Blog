---
title: "Xpath定位方式"
date: 2023-11-06T13:25:00+08:00
draft: true
author:
  name: "Jane"
comments: true
description: ""
keywords:
images:
tags:
  - Xpath
  - UI automation
---

- [xpath的教程](#xpath的教程)
- [1、基础语法](#1基础语法)
  * [1.1 基本路径](#11-基本路径)
  * [1.2 特殊符号](#12-特殊符号)
- [2、常用的xpath定位方法](#2常用的xpath定位方法)
  * [2.1 利用标签内的属性进行定位](#21-利用标签内的属性进行定位)
  * [2.2 利用XPath的轴进行定位](#22-利用XPath的轴进行定位)
  * [2.3 常用的xpath函数](#23-常用的xpath函数)

## xpath的教程
https://www.runoob.com/xpath/xpath-tutorial.html


**Xpath 对于UI automation非常重要，对Xpath的定位可以极大的影响UI automation的成功率**

## 1、基础语法

### 1.1 基本路径

| nodename | 选取此节点的所有子节点。                                   |
| -------- | ---------------------------------------------------------- |
| /        | 从根节点选取。                                             |
| //       | 从匹配选择的当前节点选择文档中的节点，而不考虑它们的位置。 |
| .        | 选取当前节点。                                             |
| ..       | 选取当前节点的父节点。                                     |
| @        | 选取属性。                                                 |

### 1.2 特殊符号

| 符号   | 描述。               |
| ------ | -------------------- |
| *      | 匹配任何元素节点。   |
| /      | 以选取若干个路径。   |
| node() | 匹配任何类型的节点。 |
| @*     | 匹配任何属性节点。   |


## 2、常用的xpath定位方法
### 2.1 利用标签内的属性进行定位
最常见为id，name，class等等，属性的类别没有特殊限制，只要能够唯一标识一个元素即可。
```xml
//a 表示选取所有a元素，加上[@id='start_handle']表示选取id属性为'start_handle'的a元素
xpath = "//a[@id='start_handle']"

//input 表示选取所有input元素，加上[@name='custName']表示选取name属性为'custName'的input元素
xpath = "//input[@name='custName']"
```

### 2.2 利用XPath的轴进行定位

| 轴名称             | 结果                                                     |
| ------------------ | -------------------------------------------------------- |
| ancestor           | 选取当前节点的所有先辈（父、祖父等）。                   |
| ancestor-or-self   | 选取当前节点的所有先辈（父、祖父等）以及当前节点本身。   |
| attribute          | 选取当前节点的所有属性。                                 |
| child              | 选取当前节点的所有子元素。                               |
| descendant         | 选取当前节点的所有后代元素（子、孙等）。                 |
| descendant-or-self | 选取当前节点的所有后代元素（子、孙等）以及当前节点本身。 |
| following          | 选取文档中当前节点的结束标签之后的所有节点。             |
| namespace          | 选取当前节点的所有命名空间节点。                         |
| parent             | 选取当前节点的父节点。                                   |
| preceding          | 选取文档中当前节点的开始标签之前的所有节点。             |
| preceding-sibling  | 选取当前节点之前的所有同级节点。                         |
| self               | 选取当前节点。                                           |

**注意要点**
- following表示选取**当前节点结束标签之后**的所有节点

- parent::可指定要查找的**当前节点的直接父节点**，例如，父节点是个div，即可写成`parent::div`,如果要找的元素不是直接父元素，则不可使用parent，可使用ancestor，代表父辈、祖父辈等节点;

- child::表示直接子节点元素

- following-sibling只会标识出当前节点结束标签之后的兄弟节点，而**不包含其他子节点**


### 2.3 常用的xpath函数

使用功能函数能够更好的进行模糊搜索

| 函数        | 用法                                                      | 解释                        |
| ----------- | --------------------------------------------------------- | --------------------------- |
| starts-with | xpath(‘//div[starts-with(@id,”ma”)]‘)                     | 选取id值以ma开头的div节点   |
| contains    | xpath(‘//div[contains(@id,”ma”)]‘)                        | 选取id值包含ma的div节点     |
| and         | xpath(‘//div[contains(@id,”ma”) and contains(@id,”in”)]‘) | 选取id值包含ma和in的div节点 |
| text()      | xpath(‘//div[contains(text(),”ma”)]‘)                     | 选取节点文本包含ma的div节点 |

