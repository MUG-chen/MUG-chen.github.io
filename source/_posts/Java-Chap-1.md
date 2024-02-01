---
title: Java-Chap.1
cover: false
tags: Java Programming
catrgories: Study Notes
summary: Java 笔记 第一部分
abbrlink: 36863
date: 2023-09-21 16:27:14
---

# Java 入门

> 本文旨在让读者大致了解Java，并对其中的一些基本内容进行说明

## 简介

> 在学习Java之前，我们首先应当了解Java的一些细节

### Java是什么？

Java是由SUN公司开发的一种编程语言，如今已被Oracle收购。

但时至今日，Java已经不仅仅是一门编程语言，Java包含着许多方面：
- 一类编程语言
- 一种开发环境
- 一种应用运行环境

得益于Java本身强大的兼容性，其不仅仅在服务器端的应用中占据着一席之地，同样在PC，移动端应用开发上有广大的应用场景。

### Java迄今的地位

迄今为止，Java在编程语言使用率上仍然占据着第四名的位置。这得益于其兼容性；易于理解的编译语言；内置的内存处理机制等等。

### Java的不同版本

SUN公司曾经为Java设定了三个版本，这种分类标准被沿用至今：
- Java SE (Standard Edition)
- Java EE (Enterprise Edition)
- Java ME (Micro Edition)

三者之间的关系为：EE > SE > ME

### 一些名词

***JDK*** 是Java Development Kit 的简称。  
***JRE*** 是Java Runtime Environment 的简称。
***JVM*** 是Java Virtual Machine 的简称。

Java在每台计算机上会内置一个虚拟机，即JVM。代码会先编译为Java字节码，而后放在JVM上运行，以此很好的保证了Java在各个平台上的兼容性。

JRE是Java运行的环境，而JDK比JRE更大一层，其中除了JRE外还内置了编译器、调试器等工具。

## 编译入门

### 配置过程

与C不同，Java的配置过程稍显复杂，也需要更多的时间与步骤。

整体而言，分为 下载JDK -> 配置环境变量 -> 运行IDE 三个步骤。

本笔记的运行全程以JDK-20为环境，在VScode上进行java的编写。  
博主在这个方面不做详细阐述，请自行上网搜索
