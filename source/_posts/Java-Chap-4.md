---
title: Java-Chap.4
cover: false
tags: Java Programming
catrgories: Study Notes
summary: Java 笔记 第四部分
abbrlink: 35903
date: 2023-10-15 22:18:30
---

# Java 面向对象

> 上一篇博文中，我们大致对类及其特点进行了些许介绍，本文中将更进一步介绍一些常用的操作与注意事项

## 类方法中参数的传递

## 类中的静态成员

试想一下，如果一个类中有这样的语句：

```java
public class Text{
    public static int count;
    public int number;
    
    public Text(){
        count = 1;
        count++;
        number = 1;
        number++;
    }
}
```

显然，上述语句中count与number的性质并不同，count是一个静态变量，只能进行一次初始化，而number是一个普通变量，可以多次初始化。

正由于这种区别的存在，我们称如count这种的变量为静态变量，其生命周期与类相同，而number这样的变量的生命周期则与其对象相同。也可以说，静态变量属于类，而常规变量属于对象。

这样的变量很特殊，在java中，可以直接通过类名在外部访问这个变量，如：

```java
System.out.println(Text.count);
```

> 类似的，如果static加在方法前，则称为 **类的方法** ，它也可以通过 类名.方法名 的形式进行外部访问。比如java中的math类，就有相关的特点。

## 单态设计模式(Singleton)

在java中常见一种特殊的类，为了保障数据的一致性，这种类的实例，在一次编译过程中仅有一个，我们称之为 **单例类** ，构造一个单例类的过程我们称之为 **单态设计模式** 。

```java
public class Company{
    private static Company instance = new Company();
    private String name;
    private Vehicle[] fleet;

    public static Company getCompany(){
        ...
        return instance;
    }

    private Company(){
        ...
    }
}
```

这种构造方法是私有的，保证了从外部无法访问相关的构造方法，此外其通过另一个静态函数getCompany来传入参数，间接进行唯一一个的Company的初始化。这样就保证了一个程序内只存在一个Company类。

## final关键字

final在java中用途繁多，主要有以下三种：
- final加在变量前，表示常量，只能进行一次赋值
- final加在方法前，表示该方法无法被重写
- final加在类前，表示该类是最终类，无法被继承（没有子类）

## 枚举类型

类似于C，java中也存在枚举类型，其定义方法为：

```java
enum Color{
    Red, Green, Blue;
}
```

## 抽象类(Abstract class)

java中涉及到一些类，它们没有具体的参数值，仅有一些方法，具体的参数需要在其子类下进行定义，我们称这种类型为 **抽象类** 。

这样的类定义需要加入 **abstract** 关键字：
```java
public abstract class <class_name>{
    ...
}
```

抽象类常用于定义同一类型的对象的相似方法。

> 其实，抽象类也可以没有抽象方法，如果这样的话，这种类就只能进行子类派生操作。

## 接口(Interfaces)

> 上文中提到了利用抽象类来定义同一类型的实体的相似方法，但如果对象类型不同，就需要利用接口了

接口用于定义不同对象的相同行为，其定义中仅有函数声明与静态常量，没有具体实现代码，需要在不同的类中重写。

接口的定义通常如下：
```java
public interface <interface_name>{
    public void function1 ();
    public int function2 ();
}
```

可见，接口的定义与C中的函数声明很相似，仅声明出这个函数的存在，不给出具体方法。

而具体需要使用接口的函数时，需要这样写出：
```java
public class <class_name> implements <interface_name>{
    //对接口函数进行重写
}
```

### 接口的默认方法

从jdk-8开始，接口中引入了默认方法，用default关键字修饰，这样的方法可以有具体的实现代码，这种特性使得接口在添加方法时不需要对所有应用接口的类进行重写，主要目的在于提高兼容性。

----

关于面向对象的内容肯定不仅仅这么多，上述博文会在进一步了解java后继续完善。

目前，本篇博文就到这里～
