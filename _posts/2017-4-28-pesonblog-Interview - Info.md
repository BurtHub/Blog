---
layout: post
title: "Java+Android+数据结构 基础知识总结 [一] "
tags: [Interview]
description: 基础知识是面试组成很重要的一部分，基础扎实的人才很受欢迎.
categories: [Interview]
---

#### 子曰：“父母之年，不可不知也。一则以喜，一则以惧。”《論語》
##### 见过很多的人为了家庭放弃工作。你是螺丝钉，你可能一辈子就在一个地方，离开了你的地方，就成了废铁。  你是金子，钻石呢？？
###### 面试的时间一般是半个小时到一个小时左右，时间很是宝贵，建议只做自己最擅长的那一部分
###### 基础知识要配合着项目经验来进行讲述，这样才会给面试官最大的尊重，也给自己一个发光的机会

#### Java基础
* TCP （Transmission Control Protocol，传输控制协议）
	
	1. 一种面向连接的、可靠的、基于字节流的传输层通信协议
	2. TCP层是位于IP层之上，应用层之下的中间层
	3. 三次握手
		1. 客户端发送SYN（SEQ=x）报文给服务器端，-> SYN_SEND。
		2. 服务器端收到SYN报文，回应一个SYN （SEQ=y）ACK(ACK=x+1）报文，->SYN_RECV。
		3. 客户端收到服务器端的SYN报文，回应一个ACK(ACK=y+1）报文，-> Established(已建立的)。
		4. 这一过程与打电话很相似，先拨号振铃，等待对方摘机说“喂”，然后才说明是谁。在一个TCP连接中，仅有两方进行彼此通信。
	
	4. 握手以后，进行传（yue）递(hui)
	5. 可靠性保证
		1. 应用数据被分割成TCP认为最适合发送的数据块（报文）
		2. 当TCP发出一个段后，它启动一个定时器，等待目的端确认收到这个报文段。如果不能及时收到一个确认，将重发这个报文段。
		3. 既然TCP报文段作为IP数据报来传输，而IP数据报的到达可能会失序，因此TCP报文段的到达也可能会失序。（自动调整顺序）
		4. ．TCP还能提供流量控制（缓冲区大小）。

* UDP （User Data Protocol，用户数据报协议）

	1. 不面向连（fu）接(ze)
	2. 全力发送
	3. 一个可以给多个发送
	4. 不保证顺序
	5. 数据报模式
	6. 丢包   [ping就是用的这个，所以网不好就丢包]

* 新浪面试题 
 
#### 写一个函数，计算两个文件的相对路径的递归算法

	String aPath = "/P/y/z/a/b/a/g/e.php";
	String bPath = "/P/y/z/a/b/a/g/c.php"; 
	情况的时候貌似不对。 
	代码可改成： 
	public String pathARelativePathB(String pathA, String pathB, int i) {
		// A相对于B ../g/e.php
		if (pathA.contains(pathB)) {
			if (i == 1) {
				return pathA.replaceAll(pathB + "/", "");
			} else {
				StringBuffer sb = new StringBuffer();
				for (int j = 1; j < i; j++)
				sb.append("../");
				return sb.append(pathA.replaceAll(pathB + "/", "")).toString();
			}
		} else {
			return pathARelativePathB(pathA, pathB.substring(0, pathB.lastIndexOf("/")), ++i);
		}
	}


*  编写一个函数用来实现输入任意一个字符串，实现对该字符串进行反转

	1.	转换成char数组，倒着输出即可[英文数字均可] [简单(la)粗暴(ji)] 
	2.	如果是中文串，编码问题就不是那么善良了
	3.	这时候，使用字符串截取类，倒着一个一个的截取即可
	4.	也可以使用整个串长度的For循环，输出指定位置的字符即可
	5.	小技巧split("")可以让整个串按字符分割
	6.	数据结构高手的想法，整个串分割后压入栈中，进行弹出就是反转
	7.	首尾交换法 比如原长度是10，那么 [0][10] | [1][9]进行交换，for循环只用跑 1/2，效率也是非常可观
	8.	欢迎大家对以上算法进行效率排序，可以在公众号中给我留言

#### Android 基础

* 场景 [Context]
	
	1. 源码分析 Activity、Service、Application都是Context的子类
	2. 分类 Activity ApplicationContext
	3. 两个有什么区别，需要显示东西的时候，就用Activity中的Context就可以，不需要显示的时候，那么使用ApplicationContext就行，当然，注意对象的引用，发生内存泄漏也不好，软引用空指针了也不好
	4. 场景，就是前台小蜜要不停的穿梭在老板的办公室，前台等地方，所以不同的场景下，小蜜能做的事情也不同
	5. 所以，要分场合的使用你的小蜜


* 四大组件 

	1.  活动(Activity)
		1.  生命周期方法调用，四种启动方式
	2.  服务(Service)
		1.  生命周期，绑定方法
	3.  广播接收者(BroadcastReceiver)
		1.  动态注册(onDestroy中解绑)和静态注册的区别，优先级
		2.  广播分类 有序(优先级大的有权利截断广播)/无序 
		3.  广播分类 本地/全局
		4.  广播分类 Sticky 粘性广播，延迟广播 权限 android.permission.BROADCAST_STICKY 
		5.  粘性广播保证后注册的接收者也可以接收到，但只保持最后一条广播
		6.  粘性广播已经很少用
	4.  内容提供者(Content Provider)
		1. Uri格式 [scheme:] [//host:port] [path] [?query][#fragment]
		2. 当外部应用需要对ContentProvider中的数据进行添加、删除、修改和查询操作时，可以使用ContentResolver类来完成，要获取ContentResolver对象，可以使用Context提供的getContentResolver()方法。
		3. 怎么描述他的功能呢，就是给别人开的后门吧


	5.  内容观察者(ContentObserver)（提供者的小弟）
		1.  观察短信、通话记录、是否飞行模式
		2.  需要频繁检测的数据库或者某个数据是否发生改变，如果使用线程去操作，很不经济而且很耗时 
		3.  在用户不知晓的情况下对数据库做一些事件，比如：悄悄发送信息、拒绝接受短信黑名单等
		4.  比如，只接受指定用户的信息
		5.  建议和Handler配合使用更新UI

* OOM [out of memory 内存溢出]

	1. 一般一个应用使用的内存不能超过默认值 32M ，小米150M..
	2. 国内的黑科技APP就不要吐槽了，大的能占你的手机 1G 运存
	3. 为什么能占这么多还不OOM，解决方式很多
	4. 保持不重要的内存进行软引用，让系统的gc自己动起来
	5. 大图加载(10M以上的大图) 得到bitmap之前先利用BitmapFactory.Options的inSampleSize的值得到压缩图片。
	6. 数据需要的时候再进行加载
	7. LruCache 设计自己的缓存去 数据单独进行管理 底层使用LinkedHashMap在使用一个对象的时候就把这个对象移动到队列头部，而且线程安全
	8. AsyncTask 它封装了Thread和Handler




* 内存泄漏 (占用的内存只增不减)-> 合理的使用你的内存

> 先简单的泄漏一下
> 第一种 [JAVA] 泄漏
> 
	1. 创建一百个对象
	2. 把这一百个对象放入集合中，放入后把原对象引用置为空
	3. 使用完集合后，这些对象还是会继续存在，造成泄漏
	4. 将对象也置为空，系统就会自动GC

> 第二种 [上下文的泄漏]
> 
	1. 静态类中使用的Context
	2. 如果静态类的生命周期长于Context生命周期 -> 泄漏     
	3. 可以使用ApplicationContext 在Application中添加一个静态工厂方法，返回ApplicationContext.
	4. Handler 造成的内存泄漏 Handler、Message 和 MessageQueue 都是相互关联在一起的
	5. 如果Handler还有没处理完的东西Activiy已经被关闭了
	6. Handler 中还继续持有这个 Activity 的引用 -> 泄漏
	7. 解决方案，Handler 对 Activity 使用软引用
	8. 使用前判断非空
	
* 

	1. 原因，在内存中有一个无法访问也无法清除的对象
	2. 危险，小的泄漏无所谓，每次泄漏一点，时间久了，手机的内存就被啃光了，明显感觉到卡顿和发热的时候，早就积少成多了
	3. 避免这些问题是高端开发人员的核心技能之一
	4. 尽量避免使用 static 成员变量，这些东西和APP生命周期一样，极其浪费系统资源
	5. 将内部类改为静态内部类
	6. 静态内部类中使用弱引用来引用外部类的成员变量
	7. Handler 更新UI使用弱引用




* ANR [Application Not Responding]

	1. 喜欢玩旧手机的人，经常看到这个
	2. 经常会问你，xx失去响应，该不该把它关了
	3. Activity 5s  broadCastReceiver 10s Service 20s
	4. 为什么，你卡到UI线程了
	5. 好的应用是不允许这个问题出现
	6. 所以，[耗时/联网/数据库]  等操作就放到工作服务和子线程中
	7. 最好办法，异步数据处理，多用缓存机制
	8. 微小的卡顿保持在100-200ms中，放心没人发现
	9. 使用进度条来保持耗时的不尴尬
	
* 