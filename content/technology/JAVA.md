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