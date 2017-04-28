---
layout: post
title: "安卓四大护法->Activity"
tags: [Android]
description: 近来回顾了一下关于Activity的生命周期，参看了相关书籍和官方文档，也有了不小的收获. 
categories: [Android]
---

#### 子曰：溫故而知新，可以為師矣。《論語》
##### 学习技术也一样，对于技术文档或者经典的技术书籍来说，指望看一遍就完全掌握，那基本不大可能，所以我们需要经常回过头再仔细研读几遍，以领悟到作者的思想精髓。

##### 近来回顾了一下关于Activity的生命周期，参看了相关书籍和官方文档，也有了不小的收获，对于以前的认知有了很大程度上的改善，在这里和大家分享一下官方文档的摘抄。

* Activity 是一个应用组件，用户可与其提供的屏幕进行交互，以执行拨打电话、拍摄照片、发送电子邮件或查看地图等操作。 每个 Activity 都会获得一个用于绘制其用户界面的窗口。窗口通常会充满屏幕，但也可小于屏幕并浮动在其他窗口之上。 

* 一个应用通常由多个彼此松散联系的 Activity 组成。 一般会指定应用中的某个 Activity 为“主” Activity，即首次启动应用时呈现给用户的那个 Activity。 而且每个 Activity 均可启动另一个 Activity，以便执行不同的操作。 每次新 Activity 启动时，前一 Activity 便会停止，但系统会在堆栈（“返回栈”）中保留该 Activity。 当新 Activity 启动时，系统会将其推送到返回栈上，并取得用户焦点。 返回栈遵循“后进先出”堆栈机制，因此，当用户完成当前 Activity 并按“返回”  按钮时，系统会从堆栈中将其弹出（并销毁），然后恢复前一 Activity。（任务和返回栈文档中对返回栈有更详细的阐述。） 

* 当一个 Activity 因某个新 Activity 启动而停止时，系统会通过该 Activity 的生命周期回调方法通知其这一状态变化。Activity 因状态变化—系统是创建 Activity、停止 Activity、恢复 Activity 还是销毁 Activity— 而收到的回调方法可能有若干种，每一种回调方法都会为您提供执行与该状态变化相应的特定操作的机会。 例如，停止时，您的 Activity 应释放任何大型对象，例如网络或数据库连接。 当 Activity 恢复时，您可以重新获取所需资源，并恢复执行中断的操作。 这些状态转变都是 Activity 生命周期的一部分。 

#### 创建 Activity
* 要创建 Activity，您必须创建 Activity 的子类（或使用其现有子类）。您需要在子类中实现 Activity 在其生命周期的各种状态之间转变时（例如创建 Activity、停止 Activity、恢复 Activity 或销毁 Activity 时）系统调用的回调方法。 两个最重要的回调方法是： 
onCreate()您必须实现此方法。系统会在创建您的 Activity 时调用此方法。您应该在实现内初始化 Activity 的必需组件。 最重要的是，您必须在此方法内调用 setContentView()，以定义 Activity 用户界面的布局。onPause()系统将此方法作为用户离开 Activity 的第一个信号（但并不总是意味着 Activity 会被销毁）进行调用。 您通常应该在此方法内确认在当前用户会话结束后仍然有效的任何更改（因为用户可能不会返回）。 
您还应使用几种其他生命周期回调方法，以便提供流畅的 Activity 间用户体验，以及处理导致您的 Activity 停止甚至被销毁的意外中断。

#### 实现用户界面

* Activity 的用户界面是由层级式视图—衍生自 View 类的对象—提供的。每个视图都控制 Activity 窗口内的特定矩形空间，可对用户交互作出响应。 例如，视图可以是在用户触摸时启动某项操作的按钮。 

* 您可以利用 Android 提供的许多现成视图设计和组织您的布局。“小工具”是提供按钮、文本字段、复选框或仅仅是一幅图像等屏幕视觉（交互式）元素的视图。 “布局”是衍生自 ViewGroup 的视图，为其子视图提供唯一布局模型，例如线性布局、网格布局或相对布局。您还可以为 View 类和 ViewGroup 类创建子类（或使用其现有子类）来自行创建小工具和布局，然后将它们应用于您的 Activity 布局。

* 利用视图定义布局的最常见方法是借助保存在您的应用资源内的 XML 布局文件。这样一来，您就可以将用户界面的设计与定义 Activity 行为的源代码分开维护。 您可以通过 setContentView() 将布局设置为 Activity 的 UI，从而传递布局的资源 ID。不过，您也可以在 Activity 代码中创建新 View，并通过将新 View 插入 ViewGroup 来创建视图层次，然后通过将根 ViewGroup 传递到 setContentView() 来使用该布局。
#### 在清单文件中声明 Activity
* 使用 Intent 过滤器


		<activity android:name=".ExampleActivity" android:icon="@drawable/app_icon">
		    <intent-filter>
		        <action android:name="android.intent.action.MAIN" />
		        <category android:name="android.intent.category.LAUNCHER" />
		    </intent-filter>
		</activity>

#### 启动 Activity
* 您可以通过调用 startActivity()，并将其传递给描述您想启动的 Activity 的 Intent 来启动另一个 Activity。Intent 对象会指定您想启动的具体 Activity 或描述您想执行的操作类型（系统会为您选择合适的 Activity，甚至是来自其他应用的 Activity）。 Intent 对象还可能携带少量供所启动 Activity 使用的数据。 

* 在您的自有应用内工作时，您经常只需要启动某个已知 Activity。 您可以通过使用类名创建一个显式定义您想启动的 Activity 的 Intent 对象来实现此目的。 例如，可以通过以下代码让一个 Activity 启动另一个名为 SignInActivity 的 Activity：

	Intent intent = new Intent(this, SignInActivity.class);
	startActivity(intent);

不过，您的应用可能还需要利用您的 Activity 数据执行某项操作，例如发送电子邮件、短信或状态更新。 在这种情况下，您的应用自身可能不具有执行此类操作所需的 Activity，因此您可以改为利用设备上其他应用提供的 Activity 为您执行这些操作。 这便是 Intent 对象的真正价值所在—您可以创建一个 Intent 对象，对您想执行的操作进行描述，系统会从其他应用启动相应的 Activity。 如果有多个 Activity 可以处理 Intent，则用户可以选择要使用哪一个。 例如，如果您想允许用户发送电子邮件，可以创建以下 Intent 对象： 
Intent intent = new Intent(Intent.ACTION_SEND);
intent.putExtra(Intent.EXTRA_EMAIL, recipientArray);
startActivity(intent);

添加到 Intent 中的 EXTRA_EMAIL extra 是一个字符串数组，其中包含应将电子邮件发送到的电子邮件地址。 当电子邮件应用响应此 Intent 时，它会读取 extra 中提供的字符串数组，并将它们放入电子邮件撰写窗体的“收件人”字段。 在这种情况下，电子邮件应用的 Activity 启动，并且当用户完成操作时，您的 Activity 会恢复执行

#### 启动 Activity 以获得结果
* 有时，您可能需要从启动的 Activity 获得结果。在这种情况下，请通过调用 startActivityForResult()（而非 startActivity()）来启动 Activity。 要想在随后收到后续 Activity 的结果，请实现 onActivityResult() 回调方法。 当后续 Activity 完成时，它会使用 Intent 向您的 onActivityResult() 方法返回结果。

* 例如，您可能希望用户选取其中一位联系人，以便您的 Activity 对该联系人中的信息执行某项操作。 您可以通过以下代码创建此类 Intent 并处理结果： 

		
		private void pickContact() {
		    // Create an intent to "pick" a contact, as defined by the content provider URI
		    Intent intent = new Intent(Intent.ACTION_PICK, Contacts.CONTENT_URI);
		    startActivityForResult(intent, PICK_CONTACT_REQUEST);
		}
		
		@Override
		protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		    // If the request went well (OK) and the request was PICK_CONTACT_REQUEST
		    if (resultCode == Activity.RESULT_OK && requestCode == PICK_CONTACT_REQUEST) {
		        // Perform a query to the contact's content provider for the contact's name
		        Cursor cursor = getContentResolver().query(data.getData(),
		        new String[] {Contacts.DISPLAY_NAME}, null, null, null);
		        if (cursor.moveToFirst()) { // True if the cursor is not empty
		            int columnIndex = cursor.getColumnIndex(Contacts.DISPLAY_NAME);
		            String name = cursor.getString(columnIndex);
		            // Do something with the selected contact's name...
		        }
		    }
		}

* 上例显示的是，您在处理 Activity 结果时应该在 onActivityResult() 方法中使用的基本逻辑。第一个条件检查请求是否成功（如果成功，则resultCode 将为 RESULT_OK）以及此结果响应的请求是否已知 — 在此情况下，requestCode与随 startActivityForResult() 发送的第二个参数匹配。 代码通过查询 Intent 中返回的数据（data 参数）从该处开始处理 Activity 结果。 

* 实际情况是，ContentResolver 对一个内容提供程序执行查询，后者返回一个 Cursor，让查询的数据能够被读取。

