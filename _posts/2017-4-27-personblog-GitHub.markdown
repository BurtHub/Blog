---
layout: post
title: "使用GitHubPager搭建个人博客"
tags: [github]
categories: [Other]
---


#### 子曰：好记性不如烂笔头。《論語》
##### 博客就像那个烂笔头，每天写一点，BUG就会越来越少


*  首先，你需要有一个github帐号
> 注册流程

	1. 打开 github.com 网站（建议使用Chrome浏览器）
	2. 右键点击网页-->翻译成中文（简体）
	3. 注册邮箱，建议使用163，126，Hotmail之类的
	4. 注册成功后，进入邮箱，点击验证邮件，完成邮箱绑定
	 
	

*  第二，搭建好提交代码的环境
>  提交环境
	
	1. 下载gitbash（建议C盘） [ https://git-for-windows.github.io/ ]
	2. 安装
	3. 配置 ssh 通信 运行 git Bash 客户端，是不是找不到快捷方式，右键在随便一个文件夹下就能看到
	4. 输入cd ~/.ssh——回车（看你是否有了ssh key 密钥，有了就备份）
	5. 输入ssh-keygen -t rsa -C "your email"——直接回车，之后会让你输入github的账号密码，会出现如图所示结果，跟着上面所指示的路径，在你的电脑中找到该文件，id_rsa文件即是你的私有密钥，id_rsa.pub是共开密钥
	6. 打开你的id_rsa.pub文件，复制下里面的内容
	7. 一般这个文件会生成在 C:\Users\Administrator\.ssh 文件夹下。如果找不到，显示一下隐藏文件即可
	8. 登录进去你的github
	9. 在右上角账户那里点击头像边上的下拉，出现如图——点击settings进去，找到左侧的SSH Keys,点击new ssh key
	10. 粘贴到下面那个框就好了，上面的不用管
	11. 最后一步了，只需测试一下链接是否正常了，接着输入：ssh -T git@github.com，这时会问是否继续连接，我们输入 yes，这样，我们的git配置就完成了。

* 第三，创建博客仓库
>  新建仓库(Repositories)

	1. 找到 [Repositories] 标签 点击绿色的 [new]
	2. 输入仓库名，简介 ---> 连着的两个框
	3. 点击下面绿色的 [create Repositories]

>  设置仓库(Repositories)

	1. 点击刚创建好的仓库
	2. 进入仓库的Setting(上面那一排最右边)
	3. 找到 [Theme chooser] 选择主题
	4. 看不懂得参考上面注册流程 [第二步]


* 自定义的博客

>  蕾欧娜： 胜利就在眼前

	1. 经常做文档的都会明白，是时候找模版了
	2. 没错，博客就是模版
	3. 你要写的，只是文章
	4. 模版一切都做好了
	5. 模版地址： http://jekyllthemes.org/

* 应用模版，开始写作
> 命令有三条

* git add .
* git commit -m "message"
* git push -u origin master


	1. 先将你的仓库clone下来
	2. 点开仓库有个绿色的 [Clone or download] 按钮
	3. 怎么都是绿色。。。。。。
	4.  复制里面的链接 
	5. 任意盘符下新建一个英文名的文件夹
	6. 右键打开 [git bash]
	7. 输入 [ git clone ] 右键粘贴 回车
	8. 很神奇吧，自动创建了一个文件夹
	9. 没错，这个就是云端的仓库
	10. 把刚才下载的模版粘贴进自动创建的文件夹
	11. 输入第二条命令
	12. 输入第三条命令
* 博客文章都存放在 [ _posts ]文件夹下面 [ markdown格式 ]
* 每次写完文章 重复上面三条命令就可以提交

