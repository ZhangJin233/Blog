---
title: "Jmeter"
date: 2023-09-18T18:32:59+08:00
author:
  name: "Jane"
comments: true
description: "Jmeter"
keywords: ["Jmeter"]
images:
tags:
  - Jmeter
---


#### 1. Jmeter mac or linux启动

```bash
sh /path/to/jmeter/bin/jmeter.sh
```
更加快捷的启动方式是，直接在终端中输入 jmeter 命令。需要在bash_profile进行以下配置：

```bash
export JMETER_HOME=/path/to/jmeter export PATH=$JMETER_HOME/bin:$PATH
```
将 JMETER_HOME 替换为实际的 Apache JMeter 所在目录。
让配置生效：

```bash
source ~/.bashrc

```
{{< image src="/images/jmeter1.png" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

一切准备就绪后，您将使用CLI模式（以前称为Non-GUI mode的命令行模式 ）运行Jmeter以进行负载测试。

**不要使用GUI模式运行负载测试！**

#### 2. 运行命令常用格式

jmeter -n -t [jmx脚本路径] -l [测试输出文件路径]

参数解释：

```text
-n: 表示 non gui mode,就是非图形化模式
 
-t: 即testplan，后跟要运行的jmeter脚本的路径和脚本名称。
 
    若指定路径下没有指定名称的脚本，则自动创建。
 
    若没有路径只写脚本名称，则默认是在当前目录查找或创建。
 
-l: 后跟输出结果文件路径和结果文件名称。
 
    若指定路径下没有指定名称的脚本，则自动创建，可以生成csv或者jtl文件。
    
    若只写脚本名称，则默认是在当前目录查找或创建。
 
示例： jmeter -n -t testplan.jmx -l test.jtl
 
示例含义：以命令行模式运行当前目录下的testplan.jmx文件，并在当前目录下输出日志文件test.jtl
```

#### 3.具体步骤

这个主要是针对不会代码脚本的童鞋们或者小伙伴可以首先在图形界面将脚本调试成功，然后再在非GUI也称为 no Mode模式下运行脚本。

1.打开JMeter图形界面

2.在默认的Test Plan上创建一个Thread Group

3.在Thread Group上面添加一个Sampler,选择HTTP Request

4.在Thread Group上面添加一个View Results Tree

5.点击Run，在弹出对话框询问是否保存，点击Yes,保存脚本到桌面，Test Plant And Report.jmx

6.检查View Results Tree里面的response code 是不是200,

7.通过检查测试通过，说明测试脚本没问题，我们这里选择删除View Results Tree

8.关闭当前JMeter对话框

9.打开cmd，通过命令运行JMeter

10.输入一下命令开始执行测试