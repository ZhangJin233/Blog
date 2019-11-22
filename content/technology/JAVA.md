---
title: "JAVA"
date: 2019-06-18T18:24:25+08:00
draft: true
author:
  name: "Jane"
comments: true
description: ""
images:
tags:
  - java
---
在Java中，所有的代码必须写在类里，所以定义一个HelloWorld类。main()函数是程序执行的入口。
```java
/*hello world程序*/
public class HelloWorld {
    public static void main(String []args) {
        System.out.println("Hello World"); //打印Hello World
    }
}
```

#### **基本数据类型**####

Java语言中的基本数据类型跟其他语言类似，主要有下面几种：

- 整数类型：byte、short、int、long
- 浮点类型：float、double
- 字符型：char
- 布尔型：boolean

定义一个基本类型变量：
```java
int a = 6;
```
除此之外，Java还提供了一些封装这些基本数据类型的类，这些类实现了一些常用的功能函数，可以直接使用，常用的类：

- Integer：对应封装了基本类型int；
- Long：对应封装了基本类型long；
- Float：对应封装了基本类型float；
- Double：对应封装了基本类型double；
- Boolean：对应封装了基本类型boolean；
- String：对应封装了字符串类型char[]

举例，定义一个Integer对象：
```java
Integer oa = new Integer(6);
```
#### **数组**####
Java中，我们使用[]来定义一个数组：
```java
int a[] = new int[10]; //定义了一个长度是10的int类型数组
```
在Java中，通过如下方式访问数组中的元素：
```java
a[1] = 3; //将下标是1的数组元素赋值为3
System.out.println(a[2]); //打印下标是2的数组元素值
```
#### **流程控制**####

- if-else语句：

```java
// 用法一
int a;
if (a > 1) {
  //执行代码块
} else {
  //执行代码块
}

// 用法二
int a;
if (a > 1) {
  //执行代码块
} else if (a == 1) {
  //执行代码块
} else {
  //执行代码块
}
```
- switch-case语句，代码示例如下：

```java
int a;
switch (a) {
  case 1:
    //执行代码块
    break;
  case 2:
    //执行代码块
    break;
  default:
    //默认执行代码
}
```
- for、while循环：

```java
for (int i = 0; i < 10; ++i) {
  // 循环执行10次此代码块
}

int i = 0;
while (i < 10) {
  // 循环执行10次此代码块
}
```
- continue、braek、return，代码示例如下所示：

```java
for (int i = 0; i < 10; ++i) {
  if (i == 4) {
    continue; //跳过本次循环，不会打印出4这个值
  }
  System.out.println(i);
}

for (int i = 0; i < 10; ++i) {
  if (i == 4) {
    break; //提前终止循环，只会打印0、1、2、3
  }
  System.out.println(i);
}

public void func(int a) {
  if (a == 1) {
    return; //结束一个函数，从此处返回
  }
  System.out.println(a);
}
```
#### **类、对象**####

Java语言使用关键词class来定义一个类，类中包括成员变量（也叫做属性）和方法（也叫作函数），其中有一种特殊的函数叫做构造函数，其命名比较固定，跟类名相同。除此之外，Java语言通过new关键词来创建一个类的对象，并且可以通过构造函数，初始化一些成员变量的值。代码示例：
```java
public class Dog { // 定义了一个Dog类
  private int age; // 属性或者成员变量
  private int weight;

  public Dog(int age, int weight) { // 构造函数
    this.age = age;
    this.weight = weight;
  }

  public int getAge() { // 函数或者方法
    return age;
  }
  
  public int getWeigt() {
    return weight;
  }
  
  public void run() {
    // ...
  }
}

Dog dog1 = new Dog(2, 10);//通过new关键词创建了一个Dog对象dog1
int age = dog1.getAge();//调用dog1的getAge()方法
dog1.run();//调用dog1的run()方法
```

#### **抽象类**####

下面这段代码是一个比较典型的抽象类的使用场景（模板设计模式）。Logger 是一个记录日志的抽象类，FileLogger 和 MessageQueueLogger 继承 Logger，分别实现两种不同的日志记录方式：记录日志到文件中和记录日志到消息队列中。FileLogger 和 MessageQueueLogger 两个子类复用了父类 Logger 中的 name、enabled、minPermittedLevel 属性和 log() 方法，但因为这两个子类写日志的方式不同，它们又各自重写了父类中的 doLog() 方法。

```java

// 抽象类
public abstract class Logger {
  private String name;
  private boolean enabled;
  private Level minPermittedLevel;

  public Logger(String name, boolean enabled, Level minPermittedLevel) {
    this.name = name;
    this.enabled = enabled;
    this.minPermittedLevel = minPermittedLevel;
  }
  
  public void log(Level level, String message) {
    boolean loggable = enabled && (minPermittedLevel.intValue() <= level.intValue());
    if (!loggable) return;
    doLog(level, message);
  }
  
  protected abstract void doLog(Level level, String message);
}
// 抽象类的子类：输出日志到文件
public class FileLogger extends Logger {
  private Writer fileWriter;

  public FileLogger(String name, boolean enabled,
    Level minPermittedLevel, String filepath) {
    super(name, enabled, minPermittedLevel);
    this.fileWriter = new FileWriter(filepath); 
  }
  
  @Override
  public void doLog(Level level, String mesage) {
    // 格式化level和message,输出到日志文件
    fileWriter.write(...);
  }
}
// 抽象类的子类: 输出日志到消息中间件(比如kafka)
public class MessageQueueLogger extends Logger {
  private MessageQueueClient msgQueueClient;
  
  public MessageQueueLogger(String name, boolean enabled,
    Level minPermittedLevel, MessageQueueClient msgQueueClient) {
    super(name, enabled, minPermittedLevel);
    this.msgQueueClient = msgQueueClient;
  }
  
  @Override
  protected void doLog(Level level, String mesage) {
    // 格式化level和message,输出到消息中间件
    msgQueueClient.send(...);
  }
}
```

**抽象类的特性：**

- 抽象类不允许被实例化，只能被继承。也就是说，你不能 new 一个抽象类的对象出来（Logger logger = new Logger(…); 会报编译错误）。
- 抽象类可以包含属性和方法。方法既可以包含代码实现（比如 Logger 中的 log() 方法），也可以不包含代码实现（比如 Logger 中的 doLog() 方法）。不包含代码实现的方法叫作抽象方法。
- 子类继承抽象类，必须实现抽象类中的所有抽象方法。对应到例子代码中就是，所有继承 Logger 抽象类的子类，都必须重写 doLog() 方法。


#### **权限修饰符**####

在前面的代码示例中，我们多次用到private、public，它们和protected一起，构成了Java语言的三个权限修饰符。权限修饰符可以修饰函数、成员变量。

- private修饰的函数或者成员变量，只能在类内部使用。
- protected修饰的函数或者成员变量，可以在类及其子类内使用。
- public修饰的函数或者成员变量，可以被任意访问。

除此之外，权限修饰符还可以修饰类，下面的示例：

```java
public class Dog {// public修饰类
  private int age; // private修饰属性，只能在类内部使用
  private int weight;
  
  public Dog(int age, int weight) {
    this.age = age;
    this.weight = weight;
  }

  public int getAge() { //public修饰的方法，任意代码都是可以调用
    return age;
  }
  
  public void run() {
    // ...
  }

}
```

#### **继承**####

Java语言使用extends关键字来实现继承。被继承的类叫做父类，继承类叫做子类。子类继承父类的所有非private属性和方法。代码如下：

```java 

public class Animal { // 父类
  protected int age;
  protected int weight;
  
  public Animal(int age, int weight) {
    this.age = age;
    this.weight = weight;
  }
  
  public int getAge() { // 函数或者方法
    return age;
  }
  
  public int getWeigt() {
    return weight;
  }
  
  public void run() {
    // ...
  }
}

public class Dog extends Animal { // 子类
  public Dog(int age, int weight) { // 构造函数
    super(age, weight); //调用父类的构造函数
  }

  public void wangwang() {
    //...
  }
}

public class Cat extends Animal { //子类
  public Cat(int age, int weight) { // 构造函数
    super(age, weight); //调用父类的构造函数
  }
  
  public void miaomiao() {
    //...
  }
}

//使用举例
Dog dog = new Dog(2, 8);
dog.run();
dog.wangwang();
Cat cat = new Cat(1, 3);
cat.run();
cat.miaomiao();
```

#### **接口**####

Java语言通过interface关键字来定义接口。接口中只能声明方法，不能包含实现，也不能定义属性。类通过implements关键字来实现接口中定义的方法。具体示例如下：

```java 
public interface Runnable {
  void run();
}

public class Dog implements Runnable {
  private int age; // 属性或者成员变量
  private int weight;

  public Dog(int age, int weight) { // 构造函数
    this.age = age;
    this.weight = weight;
  }

  public int getAge() { // 函数或者方法
    return age;
  }

  public int getWeigt() {
    return weight;
  }

  @Override 
  public void run() { //实现接口中定义的run()方法
    // ...
  }
}
```
**接口的特性：**

- 接口不能包含属性（也就是成员变量）。
- 接口只能声明方法，方法不能包含代码实现。
- 类实现接口的时候，必须实现接口中声明的所有方法。

#### **容器**####

Java提供了一些现成的容器。容器可以理解为一些工具类，底层封装了各种数据结构。比如ArrayList底层就是数组，LinkList底层就是链表，HashMap底层就是散列表。这些容器我们可以直接拿来使用。具体代码如下：

```java
public class DemoA {
  private ArrayList<User> users;
  
  public void addUser(User user) {
    users.add(user);
  }
}
```

#### **异常处理**####

Java提供了异常出错机制，可以直接使用jdk提供的现成类，也可以自定义异常。在Java中，我们通过关键字throw来抛出一个异常，通过throws声明函数抛出异常，通过try-catch-finally语句来捕获异常。代码示例：

```java
public class UserNotFoundException extends Exception { // 自定义一个异常
  public UserNotFoundException() {
    super();
  }

  public UserNotFoundException(String message) {
    super(message);
  }

  public UserNotFoundException(String message, Throwable e) {
    super(message, e);
  }
}

public class UserService {
  private UserRepository userRepo;
  public UserService(UseRepository userRepo) {
    this.userRepo = userRepo;
  }

  public User getUserById(long userId) throws UserNotFoundException {
    User user = userRepo.findUserById(userId);
    if (user == null) { // throw用来抛出异常
      throw new UserNotFoundException();//代码从此处返回
    }
    return user;
  }
}

public class UserController {
  private UserService userService;
  public UserController(UserService userService) {
    this.userService = userService;
  }
  
  public User getUserById(long userId) {
    User user = null;
    try { //捕获异常
      user = userService.getUserById(userId);
    } catch (UserNotFoundException e) {
      System.out.println("User not found: " + userId);
    } finally { //不管异常会不会发生，finally包裹的语句块总会被执行
      System.out.println("I am always printed.");
    }
    return user;
  }
}
```

#### **package包**####

Java通过package关键字来分门别类的组织类，通过import关键字来引入类或者package。具体代码如下：

```java
/*class DemoA*/
package com.xzg.cd; // 包名com.xzg.cd

public class DemoA {
  //...
}

/*class DemoB*/
package com.xzg.alg;

import java.util.HashMap; // Java工具包JDK中的类
import java.util.Map;
import com.xzg.cd.DemoA;

public class DemoB {
  //...
}
```