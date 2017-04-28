---
layout: post
title: "jekyll 基于 Ruby 的本地博客系统"
tags: [Ruby]
categories: [Ruby]
---

#### 子曰：“语之而不惰者，其回也与！”《論語》
##### 学过JS的同学特别庆幸的一件事就是 - 变量没有类型 - 完全面向对象 - 任何东西都有值 - 适合于快速开发，一般开发效率是JAVA的5倍
* ruby（红宝石）优雅的一门动态语言。
* 没错，上面的特性就是我从Ruby特性里复制的


##### 首先安装Ruby
* 下载地址： http://rubyinstaller.org/downloads/
* 安装，记得勾选上 [Add Ruby executables to your PATH]
* 上面的选项就是自动创建环境变量，经历过[JAVA_HOME]。。的同学请举手
* 下载第二个： https://rubygems.org/pages/download
* 选ZIP格式就行，下的飞快
* 任意一个文件夹，解压后，按win徽标+R，输入CMD
* cd 到刚才解压的文件夹，输入 ruby set+ Tab键自动补齐
* ruby setup.rb 完成后 输入 gem install jekyll 
* 两个都安装完毕，好了，现在你的电脑已经准备完毕了。

##### 让本地服务器飞起来
* http://jekyllthemes.org/ 下载你喜欢的模版到任意目录
* $ cd you website path //cd到你的上一句的任意目录下
* $ jekyll serve
* 一个开发服务器将会运行在 http://localhost:4000/
* 你就能在本地服务器看到你用模板搭建的网站了
* 愉快的修改吧