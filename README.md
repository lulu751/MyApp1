# MyApp1
一、Activity的基本概念
　　Activity是Android的四大组件之一，它是一种可以包含用户界面的组件，主要用于和用户进行交互，比如打电话，照相，发送邮件，或者显示一个地图！Activity用于显示用户界面，用户通过Activity交互完成相关操作 ， 一个App允许有多个Activity。
  
  

二、Activity的生命周期
　　Activity生命周期是每一个Android开发者都必须掌握的，当我们深入理解活动的生命周期之后，就可以写出更加连贯流畅的程序，让我们的程序拥有更好的用户体验
　　您可以通过实现这些方法监控 Activity 生命周期中的三个嵌套循环：

Activity 的整个生命周期发生在 onCreate() 调用与 onDestroy() 调用之间。您的 Activity 应在 onCreate() 中执行“全局”状态设置（例如定义布局），并释放 onDestroy() 中的所有其余资源。例如，如果您的 Activity 有一个在后台运行的线程，用于从网络上下载数据，它可能会在 onCreate() 中创建该线程，然后在 onDestroy() 中停止该线程。
Activity 的可见生命周期发生在 onStart() 调用与 onStop() 调用之间。在这段时间，用户可以在屏幕上看到 Activity 并与其交互。 例如，当一个新 Activity 启动，并且此 Activity 不再可见时，系统会调用 onStop()。您可以在调用这两个方法之间保留向用户显示 Activity 所需的资源。 例如，您可以在 onStart() 中注册一个 BroadcastReceiver 以监控影响 UI 的变化，并在用户无法再看到您显示的内容时在 onStop() 中将其取消注册。在 Activity 的整个生命周期，当 Activity 在对用户可见和隐藏两种状态中交替变化时，系统可能会多次调用 onStart() 和 onStop()。

Activity 的前台生命周期发生在 onResume() 调用与 onPause() 调用之间。在这段时间，Activity 位于屏幕上的所有其他 Activity 之前，并具有用户输入焦点。 Activity 可频繁转入和转出前台 — 例如，当设备转入休眠状态或出现对话框时，系统会调用 onPause()。 由于此状态可能经常发生转变，因此这两个方法中应采用适度轻量级的代码，以避免因转变速度慢而让用户等待。

图 1 说明了这些循环以及 Activity 在状态转变期间可能经过的路径。矩形表示回调方法，当 Activity 在不同状态之间转变时，您可以实现这些方法来执行操作。


![图一](https://img-blog.csdnimg.cn/20190313214600981.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2x1X2x1X3poYW5n,size_16,color_FFFFFF,t_70)

三、协调 Activity
当一个 Activity 启动另一个 Activity 时，它们都会体验到生命周期转变。第一个 Activity 暂停并停止（但如果它在后台仍然可见，则不会停止）时，同时系统会创建另一个 Activity。 如果这些 Activity 共用保存到磁盘或其他地方的数据，必须了解的是，在创建第二个 Activity 前，第一个 Activity 不会完全停止。更确切地说，启动第二个 Activity 的过程与停止第一个 Activity 的过程存在重叠。

生命周期回调的顺序经过明确定义，当两个 Activity 位于同一进程，并且由一个 Activity 启动另一个 Activity 时，其定义尤其明确。 以下是当 Activity A 启动 Activity B 时一系列操作的发生顺序：

Activity A 的 onPause() 方法执行。
Activity B 的 onCreate()、onStart() 和 onResume() 方法依次执行。（Activity B 现在具有用户焦点。）
然后，如果 Activity A 在屏幕上不再可见，则其 onStop() 方法执行。
您可以利用这种可预测的生命周期回调顺序管理从一个 Activity 到另一个 Activity 的信息转变。 例如，如果您必须在第一个 Activity 停止时向数据库写入数据，以便下一个 Activity 能够读取该数据，则应在 onPause() 而不是 onStop() 执行期间向数据库写入数据。
四、 项目运行截图

![第一次启动项目](https://img-blog.csdnimg.cn/20190313214905127.png)

![退出项目](https://img-blog.csdnimg.cn/20190313214943122.png)

![重新打开项目](https://img-blog.csdnimg.cn/20190313215006171.png)

