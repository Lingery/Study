# 01Java语言概述

[TOC]

## Java语言发展史

· 创造者：詹姆斯·高斯林（James Gosling） 

### SUN

* (Stanford University Network斯坦福大学网络公司)
* 1995年5月23日，Java语言诞生
* 1996年1月	JDK1.0
* 1997年2月	JDK1.1
* 1998年12月JDK1.2(将Java分成了J2SE,J2EE,J2ME)
* 2000年5月	J2SE1.3
* 2002年2月	J2SE1.4
* 2004年10月 JDK1.5(改名JavaSE5.0,JavaEE,JavaME)
* 2006年12月JavaSE6.0
* 2009年04月20日，甲骨文(Oracle)74亿美元收购Sun。
* 2011年7月 	JavaSE7.0
* 2014年3月	JavaSE8.0

## Java语言平台

### J2SE(Java 2 Platform Standard Edition)标准版

* 为开发普通桌面和商务应用程序提供的解决方案,该技术体系是其他两者的基础，可以完成一些桌面应用程序的开发

### J2ME(Java 2 Platform Micro Edition)小型版

* 为开发电子消费产品和嵌入式设备提供的解决方案

###  J2EE(Java 2 Platform Enterprise Edition)企业版

* 为开发企业环境下的应用程序提供的一套解决方案,该技术体系中包含的技术如 Servlet、Jsp等，主要针对于Web应用程序开发 

## Java语言跨平台原理

- 平台：即操作系统(Windows，Linux，Mac)
- 跨平台：Java程序可以在任意操作系统上运行，一次编写到处运行
- 原理：实现跨平台需要依赖Java的虚拟机 JVM （Java Virtual Machine）

![Java语言跨平台原理](./images/01/01Java.png)

## JRE和JDK

![JRE和JDK](./images/01/02JRE.jpg)

## 常用DOS命令

###打开控制台

- win + R，然后cmd回车

### 常用命令

- d: 回车	盘符切换
- dir(directory):列出当前目录下的文件以及文件夹
- cd (change directory)改变指定目录(进入指定目录)
- 进入	cd 目录；cd 多级目录
- 回退	cd.. 或 cd\
- cls : (clear screen)清屏
- exit : 退出dos命令行

## JDK的下载及安装

## Path环境变量的配置

- 为什么要配置
程序的编译和执行需要使用到javac和java命令，所以只能在bin目录下写程序
实际开发中，不可能把程序写到bin目录下，所以我们必须让javac和java命令在任意目录下能够访问
- 如何配置
创建新的变量名称：JAVA_HOME
计算机-右键属性-高级系统设置-高级-环境变量-系统变量
为JAVA_HOME添加变量值：JDK安装目录
在path环境变量最前面添加如下内容
%JAVA_HOME%\bin;

## HelloWorld案例

完整代码：HelloWorld.java
```
public class HelloWorld {
	public static void main(String [] args) {
		System.out.println(“HelloWorld”);
	}
}
```

- 在命令行模式中，输入javac命令对源代码进行编译，生成字节码文件
		javac HelloWorld.java
- 编译完成后，如果没有报错信息，输入java命令对class字节码文件进行解释运行,执行时不需要添加.class扩展名
		java HelloWorld

