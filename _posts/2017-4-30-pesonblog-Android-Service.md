---
layout: post
title: "Android 四大护法-> Service"
tags: [Android]
description: 感觉到手机明显的卡顿的时候，又看不见开了什么程序，那么你就该警惕了，多半是后台看不见得服务在做怪。
categories: [Android]
---

#### 子曰：“温故而知新，可以为师矣。！”《論語》
##### Service作为Android四大组件之一，在每一个应用程序中都扮演着非常重要的角色。它主要用于在后台处理一些耗时的逻辑，或者去执行某些需要长期运行的任务。必要的时候我们甚至可以在程序退出的情况下，让Service在后台继续保持运行状态。


##### 常见生命周期
##### 既然是四大护法，明显都是有生命的
* A started service 
> 　启动服务

	1. 被开启的service通过其他组件调用 startService()被创建。
	2. 这种service可以无限地运行下去，必须调用stopSelf()方法或者其他组件调用stopService()方法来停止它。
	3. 当service被停止时，系统会销毁它。

* A bound service
>  绑定服务

	1.　被绑定的 service 是当其他组件（一个客户）调用 bindService() 来创建的。
	2.　客户可以通过一个IBinder接口和 service 进行通信。　
	3.　客户可以通过 unbindService()方法来关闭这种连接。
	4.　一个 service 可以同时和多个客户绑定，当多个客户都解除绑定之后，系统会销毁 service。 
	5.　当服务被绑定到客户的时候，stopService() 或 stopSelf()实际上并不能停止这个 service，除非所有的客户都解除绑定。
	6.　已经启动的 service 才能进行绑定操作

* 活跃时间 
>  The entire lifetime

	1. service整体的生命时间是从onCreate()被调用开始，到onDestroy()方法返回为止。
	2. 和activity一样，service在onCreate()中进行它的初始化工作，在onDestroy()中释放残留的资源。
	3. 　比如，一个音乐播放service可以在onCreate()中创建播放音乐的线程，在onDestory()中停止这个线程。
	4. 　　onCreate() 和 onDestroy()会被所有的service调用，不论service是通过startService()还是bindService()建立。

> The active lifetime

	1. service积极活动的生命时间（active lifetime）是从onStartCommand() 或onBind()被调用开始，它们各自处理由startService()或 bindService()方法传过来的Intent对象。
	2. 如果service是被开启的，那么它的活动生命周期和整个生命周期一同结束。
	3. 如果service是被绑定的，它们它的活动生命周期是在onUnbind()方法返回后结束。
	4. 因此，如果你的service是一个纯粹的绑定service，那么你不需要管理它的生命周期。
	5. onRebind()的返回值为void，但是客户端仍然在它的 onServiceConnected()回调方法中得到 IBinder 对象。



> Binding to a Service

	1. 绑定过程是异步的（asynchronous） ， bindService()方法会立即返回，但是不会返回IBinder对象给客户端。
	2. 为了接收到IBinder，客户端必须创建一个ServiceConnection的实例，并且把它传给 bindService()，这个 ServiceConnection中会包含一个回调函数，系统调用它来传递 IBinder对象。
	3. 仅仅是activity，service和content provider可以和service绑定
	4. 实现ServiceConnection
	5. 　onServiceDisconnected() 当和service的连接意外丢失时，系统会调用这个方法。如果是客户端解除绑定，系统不会调用这个方法。
	6. 　如果你想要你的activity即便在后台停止时仍然接收响应，你可以在onCreate()中绑定，在onDestroy()中解除绑定。


　　

 　


　

　

　　
　　
　　