---
title: Java-Chap.3
cover: false
tags: Java Programming
catrgories: Study Notes
summary: Java 笔记 第三部分
abbrlink: 20094
date: 2023-10-15 22:06:30
---

# Java 类与方法

## 类

### 类是什么

**类** 有些类似C中的结构体，不过Java中的类除了变量外，也可以包含函数，我们称之为 **方法** 。

> 如果读者接触过C++，那么可以将类理解为一种 **模板** ，而每个实例都是对于模板的一种创建过程。

### 类的特点与必要性

类的代码可重用，这极大程度上降低了代码语言的重复性，同时有效提高了便捷度。  
通常而言，Java中的类具有以下三种特点：
- 继承性
- 多态性
- 封装性

这三种特点的具体表现将在以下详细阐述。

### 类的定义 & 实例的声明

Java是面向对象的编程语言，这就意味着类是Java中的基础构成部分，任何一个Java程序均离不开类。

```java
[public / private] [abstract / final] class <class_name> [extends class_name]{
    <property_type> var1;
    <property_type> var2;
    
    function1 ();
    function2 ();
}

//若在编写中需要使用这个类，则利用以下语句进行声明：
<class_name> <var_name> = new <class_name>;
```

上述语句能够表示一个Java类的定义，其中public / private 表示类的访问权限，abstract / final表示类是否为抽象类 / 是否能被继承，内部的var1 表示变量声明，而后的function表示方法（具体函数）。

如同我们此前讲过的那样，Java类中可以声明所有的数据类型，但在声明过后，如果不进行初始化，Java会使用 **默认值自动对其进行初始化操作** ，默认值如下：
- int: 0
- double / float: 0.0
- char: "\u0000"
- boolean: false
- 数组: NULL

除此之外，Java中的类允许 **方法** 的定义，类似于C中的一个函数，可以进行这种类中可能涉及的操作，并返回相应的值。

与此同时，Java的类，类中的变量声明，类中的方法定义，均可以在前方添加 **访问控制符** 具体请看下文对于访问控制符的内容。

需要注意的是，类的名称通常使用大写字母开头，请尽可能养成这样的习惯，这有利于我们的程度可读性。

### 类中的构造函数与this关键字

在Java中的类中，常见用private对其内变量进行修饰，以此保证类的运行安全性。这种定义方式被称为 **类的封装** 。但这样做的后果是，无法从类的外部对类内部的变量直接进行更改，因此，Java的类提供了一种 **构造函数** 的方法，它与类同名，可以接受外部参数并以此根据其规则改变内部参量。

```java
public class Teacher{
    private int age;
    private String name;
    
    public Teacher(int age, String name){
        this.age = age;
        this.name = name;
    }
}
```

我们可以看出，在这里，从外部传入的参数叫age，name，但对象内也有叫做同样名字的参量。因此，Java引出了 **this** 关键字，在变量名前方加入this. ，则表示指向 **当前对象内的参数** 。我们能通过这样的特性，对类内的私有参量进行赋值。

对类的封装能够使编译者或程序使用者在对类进行操作时更有条理，也避免了外部随意修改类内部代码的情况。

此外，在一个类中的一个方法需要利用其所在类内的另一个方法时，可以使用<this.method_name>来对其进行调用。

### 类中方法的重载

Java中的类允许存在多个重名的方法，这被称为 **重载(Overload)** ，而重载的要求为两个同名函数的参数列表必须有区别。

### 可变长度参数

Java类中的方法允许传入多个同类型的参数，具体定义方法如下：
```java
public void setnames(String... names){
    ...
}
```

利用这样的定义，可以直接传入多个String。

这里提供另一种写法，其用途与上述定义相似，区别在于其基于数组传入参数，因此从外部调用时需要先行构造数组：

```java
public void setnames(String[] names){
    ...
}
```

### 访问控制修饰符

为了考虑一个文件，一个类在其他位置的访问权限，Java中提出了 **访问控制修饰符** 的概念。

Java有4类访问控制修饰符：
- private：仅仅允许同一个类中的方法来访问。
- default：同一个包里文件都可以访问。
- protected：不仅仅同一个包中，只要是它的子类，均可以访问。
- public：完全公开。

此外，Java中规定了，在一个源文件中（.java）， **允许且仅允许** 一个 **public** 类的存在，请在编写中注意这一点。

## 继承

### 什么是继承

当两个类具有相同的属性时，我们往往可以使用 **继承** 的方法进行定义。  
这种情况下，有父类与子类之分，子类具有父类的全部属性和方法，同时也可以进行相应更具体属性、方法的添加。

这种方法常用 **extends** 关键字来进行操作。
```java
protected class Animal{
......
}

protected class Cat extends Animal{
...
}
```

在Java中，所有后方没有进行extend的类，都会在编译时自动扩展为 **extends Object** ，这是因为Object类是java中所有类的父类，是个默认定义。因此，Java中除了Object类之外，严格来说其他的类均有父类。

当然，这其中也必然涉及到一些父类的属性我们不希望继承到子类中，或者希望在子类中对父类的方法进行覆盖，这就涉及到修饰符的问题了。

>额外提一句，其实C++中有继承的方法，并且允许多亲继承，即一个子类有多个父类，但这种方法在两个父类的方法名相同时会引起冲突。Java考虑到了这一点，并不允许多亲继承。

### super关键字

我们也会遇到，在子类中已经对父类的方法进行覆盖，但我们仍然希望调用父类中的特定方法的情况，我们常用 **super** 来进行操作。

```java
public class Father{
    protected String getdetails(){
    }
}

public class Child extends Father{
    private String getdetails(){
        String x = super.getdetails() + "Manager";
        return x;
    }
}
```

### 子类的构造方法

Java基于子类必须基于父类这一原则，声明了子类的构造方法必须首先调用父类的构造方法，这种构造可以是显性的，也可以是隐性的。

这就代表着子类的构造函数必定会对父类的构造函数进行引用，而这里也常常出现一个很不容易发现的问题：  
如果父类中没有无参的构造方法，而子类中的构造方法内又没有明确声明要使用父类的哪种有参构造方法，则每次构造子类对象时，都会默认先调用父类的无参构造方法，这就导致了编译错误。

这段话听起来有点绕腾：

```java
class Preson{
    protected String name;
    protected int age;

    public Preson(String name, int age){
        ...
    }
}

class Student{
    protected int score;

    public Student(String name, int age, int score){
        this.name = name;
        this.age = age;
        this.score = score;
    }
}
```

如上的代码是会报错的，因为其子类的构造方法在编译过程中会默认在最前方加一句：
```java
super();
```
用于先对父类的构造方法进行访问。而这里父类没有无参构造方法。

因此，请在父类中写出无参构造方法，或者在子类中申明一个构造方法，使用super关键字，对父类的含参构造方法进行调用。

### final / sealed & permits

Java中，可以用final或sealed来对类进行修饰，分别表示 **该类不允许进一步继承** 以及 **只允许指定类继承** 。

```java
public sealed class Person permits Student, Teacher{
    //表示Person类只允许Student以及Teacher类进行继承
    ...
}

public final class Student{
    //表示Student类不允许再进一步被继承
    ......
}
```

### 向上转型(Upcasting) & 向下转型(Downcasting) & instanceof

由于Java中子类具有父类的全部功能，因此在Java中定义一个父类对象，让其指向子类，这是 **被允许的** 。

比如，拿上文中的类举例子：
```java
Student s = new Student();
Person p = s;
```
这是可以的。

但是，当我们想反过来的时候，这个操作就不一定能成了：

```java
Person s1 = new Student();
Person s2 = new Person();
Student s3 = s1; //允许，因为s1实质上指向的是一个Student对象
Student s4 = s2; //不允许，因为s2实质上指向的是一个Person对象
```

因此，为了确保向下转型不会出错，java提供了一种操作符叫 **instanceof**。

```java
s1 instanceof Student;
```

上述语句可以判断s1对象指向的到底是不是Student，并返回相应的布尔变量。

从Java 14开始，可以直接在判断的类后面加名字，从而达成直接转型：

```java
if(s1 instanceof Student stu1){
    System.out.println(stu1.name);
}
```

可以看到，如果s1是Student，会直接转型为stu1，并执行输出语句。

## 多态

### 子类对父类方法的覆写(Override)

在子类中，如果希望对父类中的某个方法进行重写，可以进行 **Override** 操作。

具体方法为：在子类中定义一个与父类的某一个方法
- 方法名相同
- 返回类型相同（也可以返回该类型的子类型）
- 参数列表相同

的方法。

>子类中覆盖父类的方法，其访问限制必须要比父类的相应方法更宽泛。如：
```java
public class Father{
    protected int getdetails(){
    }
}

public class Child extends Father{
    private int getdetails(){
    }
}
```
>这种定义是不被允许的。

### 覆写与转型

我们不妨设想这样一种情况：
```java
class Person {
    public void get_age(){
        ...
    }
}

class Student extends Person{
    public void get_age(){
        ...
    }
}

Person p1 = new Stuent();
p1.get_age();
```

不妨想一想这时候调用的是哪一个get_age方法？

事实证明，Java中调用方法是根据对象的实际类型来调用的，而非其声明类型。

这就引出了一个很重要的概念。

### 多态是个啥

上文中，我们知道了Java在调用方法时，会根据对象的实际类型决定调用什么方法。

这就是多态的重要特性， **针对某个类型的方法调用，其真正执行的方法取决于运行时期实际类型的方法** 。

这使得，如果我们定义某个函数：

```java
public void get_all_name(Person s1){
    s1.get_name();
}
```

这样的一个函数可以传入Person类，也同样可以传入Person的子类Student类，而在调用它们的get_name()方法时，Java会自动根据其实际类型来决定调用什么方法，这为我们省去了很多麻烦。

### 异构集合体

```java
Employee[] list = new Employee[200];
list[0] = new Employee();
list[1] = new Manager();  //Manager 是Employee的子类
```

这种定义是合法的。

可以看出，这个集合中不仅仅存在Employee类型，还存在其子类Manager类型。  
但当我们需要对其进行操作时，我们需要得知当前操作的对象到底是什么类型，此时，我们常用前文中的 **instanceof** 关键字来确定一个对象到底是否是某个类型。



----

这篇博文写的比较仓促，可能会存在诸多不足之处，博主会在后续空闲时间尽力补足。

下一篇博文会涉及到更深入一些的面向对象的操作，这篇博文先到这里~