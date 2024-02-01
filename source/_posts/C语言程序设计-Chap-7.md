---
title: C语言程序设计-Chap.7
summary: C语言第七章：动态数据结构 笔记
categories: Study Notes
cover: false
abbrlink: 33475
date: 2023-02-16 00:00:00
tags: C programming
---

# 动态数据结构

## 1. 动态存储管理

### 问题阐述

在此前的编程过程中，我们所声明的存储大小都是静态的，数组有大小，变量有类型。这固然已经能够满足很多需求，但相应的，有些数据大小未知的情形我们便无法很完美的解决。在此举一例：

```c
int n;
scanf_s("%d", &n);
int student[n];
//这种先输入再创建的情况是不合规的。
```

此前，我们的解决方法大多都是创建一个足够大的数组，从而能够达成目标，但这样做势必会浪费许多存储空间。

因此，引入我们的正题——动态存储分配。

### 动态存储

在C语言中，动态存储主要依赖于两个标准库以及四个函数：
```c
//两个标准库：
<stdlib.h>
<malloc.h>
//四个函数：
malloc
calloc
realloc
free
```

接下来会一个个介绍

#### malloc函数

```c
int *p, n;
scanf_s("%d", &n);
p=(int *)malloc(n*sizeof(int));  //分配一个大小为n个int的存储空间，并将其首地址赋给p，如果分配失败则返回空指针。
if(p==NULL){
    exit(0);
}  //如果p是空指针，则直接退出程序，返回值0。
......
free(p);  //释放程序中被分配的空间。
```

malloc可以通过指针的形式来创建一个大小由用户自行输入的存储空间。

#### calloc函数

```c
int *p, n;
scanf_s("%d", &n);
p=(int *)calloc(n, sizeof(int));  //务必注意calloc函数与malloc函数的写法区别。
if(p==NULL){
    exit(0);
}
......
free(p);
```

calloc函数可以通过指针的方式来创建一个大小由用户自行输入的存储空间 <font color=Aqua> **并将其中的元素自动赋值为0** </font>

#### realloc函数

```c
int *p, n;
scanf_s("%d", n);
p=(int *)malloc(n*sizeof(int));
if(p==NULL){
    exit(0);
}  //通过以上的语句已经分配了一个空间
......
//现在发现原先分配的空间不够，需要重新分配。
n=n*2;  //将原先的n变为2倍。
int *q;
q=(int *)realloc(p, n*sizeof(int));  //重新分配一个大小为n的存储区域，将首地址赋值给一个新的指针q；
if(q==NULL){

}else{
    p=q;
}  //若分配失败，p仍然指向原来的存储区；若成功，p指向新存储区。
```

#### free函数

```c
free(p);  //释放原先p所指向的存储块。
```

#### 一点注意事项

1. 请务必注意区分malloc, calloc, realloc的用法以及写法区别。
2. malloc, calloc, realloc三种函数通常情况下返回的都是通用指针，因此在给具体类型指针赋值时需要进行强制类型转换（具体原理见上一章：指针）

## 2. 自定义类型

>此前提到过一种自定义类型——宏定义define，但宏定义只能做到简单的字符替换，从而在各种计算，定义中产生不可预知的后果，因此在这里给出更加通用的自定义类型。

### typedef关键字

```c
typedef unsigned long int ULI;
```

tppedef会用最后的一个词来代替前面的类型。  
常用于简化程序书写。

但是typedef在程序书写时不仅仅是简单替换，这里举一例：
```c
#define IP int * 
typedef int * P;

//若之后想要定义两个指针
IP a, b;  //等价于int *a, b; 会发现b不是指针
P m, n;  //这时候m, n都是指针
```

## 3. 结构

>C语言中虽然提供了很多变量类型，但是如果我们需要很多不同类型变量的结合体，则仅仅使用C语言提供的变量则显得效率低下。因此，产生了可以自定义的结构类型。

### 结构类型的定义

```c
typedef struct{
    double x;
    double y;
}POINT;  //这样就定义了一个名叫POINT的结构类型，之后可以直接使用
```

在程序中常用的结构可以通过上述方式来进行定义，从而简化此后需要使用相应模型时的书写过程。

需要注意的是，结构定义时其成员可以包含其他结构，如：
```c
typedef struct{
    POINT center;
    double radius;
}CIRCLE;
```

同样的，结构存在单位大小，但结构的单位大小并不是简简单单的将各个元素的大小加到一起，因此在计算结构大小时建议使用sizeof运算符。（这种状况的出现原因为结构体内的对齐问题，具体请自行搜索）

### 结构类型的访问

在C语言中，结构的访问有其规则。

如果结构类型相同，则可以直接通过整体相等来赋值  
如果需要对一个结构里的成员进行编辑，则使用 .   
这里举一例：
```c
typedef struct{
    double x;
    double y;
}POINT;

POINT A, B;
A.x=2.2;
A.y=3.2;
A=B;
```

### 结构数组

相应的，结构既然是自定义的数据类型，同样也可以定义一个以自定义结构为元素的数组。

```c
typedef struct{
    double x;
    double y;
}POINT;

POINT PT[4];  //相当于创建了一个由四个POINT组成的数组。
```

同时，与数组相似，结构数组也可以用指针表示：
```c
typedef struct{
    double x;
    double y;
}POINT;

POINT PT[4];
POINT *P;
P=PT;
//这里P就与PT数组的首地址绑定
```

引出了通过指针如何访问结构内的成员，比如我要用指针访问上述数组中第二个点中的X坐标值：

```c
(*(P+1)).x=2.2;  //这种表达过于繁琐，因此C语言提供了另一种方法
(P+1)->x=2.2;  //与上面的表达等价
```

这篇博文就到这里~~