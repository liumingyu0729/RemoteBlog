---
title: Java
date: 2019-11-12 14:32:16
tags:
---

版本
Java SE: Standard Edition
Java EE: Enterprise Edition
Java ME: Micro Edition
EE > SE > ME

术语 | 缩写 | 解释
:-: | :-: | :-:
Java Develop Kit | JDK | 编写Java程序的程序员使用的软件
Java Runtime Environment | JRE | 运行Java程序的用户使用的软件
Server JRE | —— | 在服务器上运行Java程序的软件
Standard Edition | SE | 用于桌面或简单服务器应用的Java平台
Enterprise Edition | EE | 用于复杂服务器应用的Java平台
Micro Edition | ME | 用于手机和其他小型设备的Java平台
Java FX | —— | 用于图形化用户界面的一个替代工具包，在Oracle的Java SE发布版本中提供
OpenJDK | —— | Java SE的一个免费开源实现，不包括浏览器集成或JavaFX
Java 2 | J2 | 一个过时的术语，用于描述1998年~2006年之间的Java版本
Software Development Kit | SDK | 一个过时的术语，用于描述1998年~2006年之间的JDK

数据类型

类型 | 储存需求 
:-: | :-: 
int | 4 字节
short | 2 字节
long | 8 字节
byte | 1 字节
float | 4 字节
double | 8 字节

常量
&emsp;final 
整除
&emsp;int / int 
强制类型转换
&emsp;(int) 
枚举型
&emsp;enum Size {SMALL, MEDIUM, LARGE}; 

String API
&emsp;.equals() 判断字符串相等（不能用==）
&emsp;.charAt() 字符串代码单元
&emsp;.codePointCount() 字符串码点数量（实际长度）
StringBuild
&emsp;StringBuild build = new StringBuild();
&emsp;build.append(ch);
&emsp;String str = build.toString();
大数值
&emsp;BigInteger BigDecimal 
深度拷贝
&emsp;Array.copyOf() 
命令行参数
&emsp;main(string[] args) 
多维数组（数组的数组 不规则数组）

类之间的关系
&emsp;依赖 use-a
&emsp;聚合 has-a
&emsp;继承 is-a
更改器方法 访问器方法（不修改对象）

实例域
&emsp;final 
静态域
&emsp;static 
工厂方法
&emsp;NumberFormat currencyFormatter = NumberFormat.getCurrencyInstance(); 

类导入
&emsp;java.time.LocalDate today = java.time.LocalDate.now();
&emsp;import java.util.*;
静态导入
&emsp;import static
将类放入包中
&emsp;package com.horstmann.corejava;
设置类路径
&emsp;-classpath
注释
&emsp;/** */
超类（父类 不能删除）
&emsp;super
阻止继承
&emsp;final
保护访问（子类可访问）
&emsp;proteced
Object（所有类的超类）