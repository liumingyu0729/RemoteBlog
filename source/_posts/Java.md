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

final 常量
int / int 整除
(int) 强制类型转换
enum Size {SMALL, MEDIUM, LARGE}; 枚举型
String API
&emsp;.equals() 判断字符串相等（不能用==）
&emsp;.charAt() 字符串代码单元
&emsp;.codePointCount() 字符串码点数量（实际长度）
StringBuild
&emsp;StringBuild build = new StringBuild();
&emsp;build.append(ch);
&emsp;String str = build.toString();