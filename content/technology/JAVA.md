---
title: "JAVA"
date: 2019-06-18T18:24:25+08:00
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

Java语言使用关键词class来定义一个类，类中包括成员变量（也叫做属性）和方法（也叫作函数），其中有一种特殊的函数叫做构造函数，其命名比较固定，跟类名相同。除此之外，Java语言通过new关键词来创建一个类的对象，并且可以通过构造函数，初始化一些成员变量的值。

一个类可以包含以下类型变量：

局部变量：在方法、构造方法或者语句块中定义的变量被称为局部变量。变量声明和初始化都是在方法中，方法结束后，变量就会自动销毁。

成员变量：成员变量是定义在类中，方法体之外的变量。这种变量在创建对象的时候实例化。成员变量可以被类中方法、构造方法和特定类的语句块访问。

**类变量**

**类**是描述，**对象**是实体。在类里所描述的成员变量，是位于这个类的每一个对象中的。

而如果某个成员有static关键字做修饰，它就不再属于每一个对象，而是属于整个类的了。


通过每个对象都可以访问到这些类变量和类函数，但是也可以通过类的名字来访问它们。类函数由于不属于任何对象，因此也没有办法建立与调用它们的对象的关系，就不能访问任何非static的成员变量和成员函数了。

代码示例：
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

**成员变量和类变量的区别**

由static修饰的变量称为静态变量。如果某个内容是被所有对象所共享，那么该内容就应该用静态修饰；没有被静态修饰的内容，其实是属于对象的特殊描述。

不同的对象的实例变量将被分配不同的内存空间， 如果类中的成员变量有类变量，那么所有对象的这个类变量都分配给相同的一处内存，改变其中一个对象的这个类变量会影响其他对象的这个类变量，也就是说对象共享类变量。

成员变量和类变量的区别：

   1、两个变量的生命周期不同

      成员变量随着对象的创建而存在，随着对象的回收而释放。

      静态变量随着类的加载而存在，随着类的消失而消失。

   2、调用方式不同

      成员变量只能被对象调用。

      静态变量可以被对象调用，还可以被类名调用。

   3、别名不同

      成员变量也称为实例变量。

      静态变量也称为类变量。

   4、数据存储位置不同

      成员变量存储在堆内存的对象中，所以也叫对象的特有数据。

      静态变量数据存储在方法区（共享数据区）的静态区，所以也叫对象的共享数据。

static 关键字，是一个修饰符，用于修饰成员(成员变量和成员函数)。

   特点：

   1、想要实现对象中的共性数据的对象共享。可以将这个数据进行静态修饰。

   2、被静态修饰的成员，可以直接被类名所调用。也就是说，静态的成员多了一种调用方式。类名.静态方式。

   3、静态随着类的加载而加载。而且优先于对象存在。

 

弊端：

   1、有些数据是对象特有的数据，是不可以被静态修饰的。因为那样的话，特有数据会变成对象的共享数据。这样对事物的描述就出了问题。所以，在定义静态时，必须要明确，这个数据是否是被对象所共享的。

   2、静态方法只能访问静态成员，不可以访问非静态成员。
   
   因为静态方法加载时，优先于对象存在，所以没有办法访问对象中的成员。

   3、静态方法中不能使用this，super关键字。

   因为this代表对象，而静态在时，有可能没有对象，所以this无法使用。

 

什么时候定义静态成员呢？或者说：定义成员时，到底需不需要被静态修饰呢？

成员分两种：

   1、成员变量。（数据共享时静态化）

      该成员变量的数据是否是所有对象都一样：

      如果是，那么该变量需要被静态修饰，因为是共享的数据。 
      
      如果不是，那么就说这是对象的特有数据，要存储到对象中。 

   2、成员函数。（方法中没有调用特有数据时就定义成静态）

      如果判断成员函数是否需要被静态修饰呢？

      只要参考，该函数内是否访问了对象中的特有数据：

      如果有访问特有数据，那方法不能被静态修饰。

      如果没有访问过特有数据，那么这个方法需要被静态修饰。


类变量类型：

1.局部变量：在方法、构造方法、语句块中定义的变量。其声明和初始化在方法中实现，在方法结束后自动销毁

```java
public class  ClassName{
    public void printNumber（）{
        int a;
    }
    // 其他代码
}
```
2.成员变量：定义在类中，方法体之外。变量在创建对象时实例化。成员变量可被类中的方法、构造方法以及特定类的语句块访问。

```java
public class  ClassName{
    int a;
    public void printNumber（）{
        // 其他代码
    }
}
```
3.类变量：定义在类中，方法体之外，但必须要有 static 来声明变量类型。静态成员属于整个类，可通过对象名或类名来调用。

```java
public class  ClassName{
    static int a;
    public void printNumber（）{
        // 其他代码
    }
}
```



**final 修饰变量**

一个变量可以声明为final，这样做的目的是阻止它的内容被修改。这意味着在声明final变量的时候，必须初始化它

**static和final一块用表示什么**

对于变量，表示一旦给值就不可修改，并且通过类名可以访问。对于方法，表示不可覆盖，并且可以通过类名直接访问。



#### **对象交互**####

**封装**，就是把数据和对这些数据的操作放在一起，并且用这些操作把数据掩盖起来，是面向对象的基本概念之一，也是最核心的概念。

我们有一个非常直截了当的手段来保证在类的设计的时候做到封装：

1、所有的成员变量必须是private的，这样就避免别人任意使用你的内部数据；

2、所有public的函数，只是用来实现这个类的对象或类自己要提供的服务的，而不是用来直接访问数据的。除非对数据的访问就是这个类及对象的服务。简单地说，给每个成员变量提供一对用于读写的get/set函数也是不合适的设计。


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

#### **内部类**####
- 定义在别的类内部、函数内部的类

- 内部类能直接访问外部的全部资源
  包括任何私有的成员
  外部是函数时，只能访问那个函数里final的变量




#### **匿名类**####
- 在new对象的时候给出的类的定义形成了匿名类
- 匿名类可以继承某类，也可以实现某接口
- Swing的消息机制广泛使用匿名类

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

把用来做基础派生其它类的那个类叫做父类、超类或者基类，而派生出来的新类叫做子类。Java用关键字extends表示这种继承/派生关系。

继承表达了一种is-a关系，就是说，子类的对象可以被看作是父类的对象。

比如鸡是从鸟派生出来的，因此任何一只都可以被称作是一只鸟。但是反过来不行，有些鸟是鸡，但并不是所有的鸟都是鸡。

如果你设计的继承关系，导致当你试图把一个子类的对象看作是父类的对象时显然很不合逻辑，比如你让鸡类从水果类得到继承，然后你试图说：这只本鸡是一种水果，所以这本鸡煲就像水果色拉。

这显然不合逻辑，如果出现这样的问题，那就说明你的类的关系的设计是不正确的。Java的继承只允许单继承，即一个类只能有一个父类。

**子类从父类得到了什么：**

对理解继承来说，最重要的事情是，知道哪些东西被继承了，或者说，子类从父类那里得到了什么。

答案是：所有的东西，所有的父类的成员，包括变量和方法，都成为了子类的成员，除了构造方法。

构造方法是父类所独有的，因为它们的名字就是类的名字，所以父类的构造方法在子类中不存在。除此之外，子类继承得到了父类所有的成员。

但是得到不等于可以随便使用。每个成员有不同的访问属性，子类继承得到了父类所有的成员，但是不同的访问属性使得子类在使用这些成员时有所不同：有些父类的成员直接成为子类的对外的界面，有些则被深深地隐藏起来，即使子类自己也不能直接访问。

----------------------------

下表列出了不同访问属性的父类成员在子类中的访问属性：

| 父类成员访问属性 |  在父类中的含义 |  在子类中的含义  |
| ----------- | ------------- | --------------- | 
| public | 对所有人开放 | 对所有人开放 |
| protected | 只有包内其它类、自己和子类可以访问 | 只有包内其它类、自己和子类可以访问 |
| 缺省  | 只有包内其它类可以访问 | 如果子类与父类在同一个包内：只有包内其它类可以访问 ，否则：相当于private，不能访 |
| private  | 只有自己可以访问 | 不能访问 |

---------------------------

public的成员直接成为子类的public的成员，protected的成员也直接成为子类的protected的成员。

Java的protected的意思是包内和子类可访问，所以它比缺省的访问属性要宽一些。

而对于父类的缺省的未定义访问属性的成员来说，他们是在父类所在的包内可见，如果子类不属于父类的包，那么在子类里面，这些缺省属性的成员和private的成员是一样的：不可见。

父类的private的成员在子类里仍然是存在的，只是子类中不能直接访问。

我们不可以在子类中重新定义继承得到的成员的访问属性。如果我们试图重新定义一个在父类中已经存在的成员变量，那么我们是在定义一个与父类的成员变量完全无关的变量，在子类中我们可以访问这个定义在子类中的变量，在父类的方法中访问父类的那个。尽管它们同名但是互不影响。



在构造一个子类的对象时，父类的构造方法也是会被调用的，而且父类的构造方法在子类的构造方法之前被调用。

在程序运行过程中，子类对象的一部分空间存放的是父类对象。

因为子类从父类得到继承，在子类对象初始化过程中可能会使用到父类的成员。

所以父类的空间正是要先被初始化的，然后子类的空间才得到初始化。在这个过程中，如果父类的构造方法需要参数，如何传递参数就很重要了。

构造一个子类的对象时，首先确保父类拥有的成员变量得到恰当的初始化，恰当的初始化是指：

- 1、定义初始化；
- 2、构造器

如果 既有定义初始化由有构造器，定义初始化会先做；

在继承的时候，永远先做父类的定义初始化和构造器，在做子类的。




代码如下：

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

ArrayList<String> note = new ArrayList<String>;

容器有两个类型：

容器类型

元素类型

**顺序容器**

ArrayList<String> note = new ArrayList<String>();

**对象数组**

对象数组中的每个元素都是对象的管理者而非对象本身。

**集合容器**

HashSet<String> set = new HashSet<string>();

**散列表**

HashMap<Integer,String> map = new HashMap<>();


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

#### **多态**####

**多态变量**

Java的对象变量是多态的，它能保存不止一种类型的对象。

**多态的实现方式**
方式一：重写

方式二：接口

方式三：抽象类和抽象方法

**向上造型**

一个子类的对象可以向上造型为父类的类型。即，定义父类型的引用可以指向子类的对象，但是通过父类的引用只能访问父类所定义的成员，而不能访问子类所扩展的部分。

  父类型   变量   =   new  子类()；

向上造型是多态的一种体现，同时可以使程序更简单明了。


#### **控制反转**####
- 由按钮公布一个守听者接口和一对注册/注销函数
- 你的代码实现那个接口，将守听者对象注册在按钮上
- 一旦按钮被按下，就会反过来调用你的守听者对象的某个函数 


#### **设计原则**####
1、消除重复代码

2、降低耦合

耦合这个词指的是类和类之间的联系

3、可扩展性

优秀的软件设计者的一个素质就是有预见性。什么是可能会改变的？什么是可以假设在软 件的生命期内不会改变的？

---------------------------------
参考内容：

1、中国MOOC大学 浙江大学 翁恺 面向对象程序设计——Java语言

https://www.icourse163.org/course/ZJU-1001542001

2、极客时间 
王争 设计模式之美

https://time.geekbang.org/column/intro/250
