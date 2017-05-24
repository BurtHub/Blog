---
layout: post
title: "Android新语言和JAVA的一剑情缘"
tags: [LANGUAGE]
description: Kotlin block 函数式编程三板斧 闭包 空指针安全.
categories: [LANGUAGE]
---

#### 郝生曰：“吾羡慕你无牵无挂，一生潇洒。”《眾說風雲》

###### 新语言该不该换，不急

* 安卓系统共分四大层次

	1. Linux Kernel [内核层]，提供硬件驱动（摄像头驱动之类）
	2. Libraries [运行支持库] OpenGl图形渲染, SQLite（内嵌数据库）,WebKit(浏览器内核),DVM/ART[4.4以上]虚拟机，Zygote进程的所在位置
	3. Framework [系统进程管理层/四大组件/系统服务] ActivityManager WindowManager  ViewSystem ContentProviders PackageManager ResourceManager LocationManager 
	4. Applicatoin [应用App] Phone Contacts

* 最高两层使用的是JVM的驱动层，也就是说，不管怎么换语言，JVM是肯定要兼容的
* 新的语言虽然小众，在GoogleIO大会上力推的效果还是很显著
* 就像15年的Studio，后来人们才会发现他的好处
* 但是现在，JAVA的广泛应用，还会有人放弃这一门老牌大众语言吗？
* 可能是未来的趋势
* 学习也是没错的

##### 我的Studio还是停留在2.3版本

* 对于JS有点小功底的可以试试Kotlin
* 面向对象的三个大特性都要想不起来了
* 函数式编程要主流了吗
* 空指针安全感觉比JAVA靠谱一点
* 对于程序的设计思想要理解到位
* 为什么会设计这种奇奇怪怪的东西呢
* 为什么Android不支持Python
* 我不看好这种语言，但是可以做一个不错的替代学习品


#####对于一些闭包思想的感悟
1.  闭包可以读取函数内部的变量，让这些变量的值始终保持在内存中。
1. 闭包的概念： 很像JAVA中的内部类，外部类无法对他进行访问，内部类又可以自由的访问外部类资源，但是JAVA中没有严格的闭包
1. JS中的闭包：用this关键字来访问本类资源，用that来访问Window资源，很简单的就能构成闭包
