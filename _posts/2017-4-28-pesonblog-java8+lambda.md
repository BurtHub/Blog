---
layout: post
title: "Java8 的 lambda 表达式"
tags: [JAVA]
description: Lambda表达式（也称为闭包）是Java 8中最大和最令人期待的语言改变。
categories: [JAVA]
---

#### 子夏曰： “博学而笃志， 切问而近思， 仁在其中矣。”《論語》
##### Lambda表达式（也称为闭包）是Java 8中最大和最令人期待的语言改变。它允许我们将函数当成参数传递给某个方法，或者把代码本身当作数据处理：函数式开发者非常熟悉这些概念。很多JVM平台上的语言（Groovy、Scala等）从诞生之日就支持Lambda表达式，但是Java开发者没有选择，只能使用匿名内部类代替Lambda表达式。
* 跟着我的口型： 拉姆哒嗯
* 主要关键字： [ ( Object e )-> function ]
* 看到关键字，没错，就是lambda表达式
##### 先来一个小栗子
* 农民伯伯想要测量一个苹果（pojo -> Apple）
* 第一年，苹果收成不错，想要卖好价钱,就得挑最大的
* 于是程序这样写 (Apple e) { e.getLarge();}
* 第二年，苹果收成也不错，人们喜欢挑红红的那种
* 于是程序这样写 (Apple e) { e.getColor();}
* 第三年，大众很挑剔，要又大又红的那种才肯给高价
* 于是程序这样写 (Apple e) { e.getColor()&e.getLarge();}
* 使用Lambda表达式挑选又大又红的该怎么写
* result = ( filter(Apple e1 Apple e2) -> e1.larger(e2)& e1.Colorer(e2) );
* 没有了大括号的配对，也没有缩进的痛苦，哦也
* 这只是一点小福利，我也在勤奋的学习JAVA8新特性


##### 认真学习不断进步的人类
* {[ 懒人是最聪明的 ] -> [ 聪明才会做更少的努力 & 办更多的事情]}
* Lambda表达式有返回值，返回值的类型也由编译器推理得出。
* 如果Lambda表达式中的语句块只有一行，则可以不用使用return语句，下列两个代码片段效果相同：
> Lambda
> 
Arrays.asList( "a", "b", "d" ).sort( ( e1, e2 ) -> e1.compareTo( e2 ) );

> 普通代码
>
Arrays.asList( "a", "b", "d" ).sort( ( e1, e2 ) -> {
    int result = e1.compareTo( e2 );
    return result;
} ); 

##### 闭包
* 闭包是指可以包含自由（未绑定到特定对象）变量的代码块；这些变量不是在这个代码块内或者任何全局上下文中定义的，而是在定义代码块的环境中定义（局部变量）。
* “闭包” 一词来源于以下两者的结合：要执行的代码块（由于自由变量被包含在代码块中，这些自由变量以及它们引用的对象没有被释放）和为自由变量提供绑定的计算环境（作用域）。
* 在PHP、Scala、Scheme、Common Lisp、Smalltalk、Groovy、JavaScript、Ruby、 Python、Go、Lua、objective c、swift 以及Java（Java8及以上）等语言中都能找到对闭包不同程度的支持。