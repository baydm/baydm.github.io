title: Android应用的基本组件
author: JsonYe
tags:
  - Android
categories:
  - Android基础  
copyright: true
comments: true
toc: true
date: 2015-04-29 17:35:00
---

Android系统中有著名的四大组件：Activity、Service、BroadcastReceiver、ContentProvider。一个商业的Android应用程序，通常由多个基本的组件联合组成。这四大组件，在使用的时候均需要在清单文件AndroidManifest.xml中进行注册，否则不予使用。本小节将对这些组件进行简单的介绍，使读者对Android应用开发的内容有一个大致的认识。

## 活动（Activity）


Activity是Android应用中，最直接与用户接触的组件，它负责加载View组件，使其展现给用户，并保持与用户的交互。所有的Activity组件均需要继承Activity类，这是一个Content的间接子类，包装了一些Activity的基本特性。


View组件是所有UI组件、容器组件的基类，也就是说，它可以是一个布局容器，也可以是一个布局容器内的基本UI组件。View组件一般通过XML布局资源文件定义，同时Android系统也对这些View组件提供了对应的实现类。如果需要通过某个Activity把指定的View组件显示出来，调用Activity的setContentView()方法即可，它具有多个重载方法，可以传递一个XML资源ID或者View对象。

例如：
```java
LinearLayout layout=new LinearLayout(this);
setContentView(layout)；
```
或者：
```
setContentView(R.layout.main);
```

Activity为Android应用提供了一个用户界面，当一个Activity被开启之后，它具有自己的生命周期。Activity类也对这些生命周期提供了对应的方法，如果需要对Activity各个不同的生命周期做出响应，可以重写这些生命周期方法实现。对于大多数商业应用而言，整个系统中包含了多个Activity，在应用中逐步导航跳转开启这些Activity之后，会形成Activity的回退栈，当前显示并获得焦点的Activity位于这个回退栈的栈顶。

## 服务（Service）

Service主要用于在后台完成一些无需向用户展示界面的功能实现。通常位于系统后台运行，它一般不需要与用户进行交互，因此Service组件没有用户界面展示给用户。Service主要用于完成一些类似于下载文件、播放音乐等无需用户界面与用户进行交互的功能。
与Activity组件需要继承Activity类相似，Service组件同样需要继承Service类，Service类也是Context的间接子类，其中包装了一些Service的专有特性。一个Service被运行起来之后，它将具有自己独立的生命周期，Service类中对其各个不同的生命周期提供了对应的方法，开发人员可以通过在Service中重写Service类中这些生命周期方法，来响应Service各个生命周期的功能实现。

## 广播接收器（BroadcastReceiver）

BroadcastReceiver同样也是Android系统中的一个重要组件，BroadcastReceiver代表了一个广播接收器，用于接收系统中其它组件发送的广播，并对其进行响应或是拦截广播的继续传播。
广播是一个系统级的消息，当系统环境发生改变的时候会发送一些广播供对应的程序进行接收响应，例如：接收到一条短信、开机、关机、插上充电器、插上耳机、充电完成等，均会发送一条广播供需要监听此类广播的应用进行响应。除了一些系统事件的广播，开发人员也可以自定义广播内容。但是大部分情况下，开发应用的时候主要用于接受系统广播并对其进行响应，很少需要发送自定义的广播。
使用BroadcastReceiver组件接收广播非常的简单，只需要实现自己的BroadcastReceiver子类，并重写onReceive()方法，就能完成BroadcastReceiver，而对于这个BroadcastReceiver对什么广播感兴趣，则需要对其进行另行配置。

## 内容提供者（ContentProvider）
Android系统作为一个智能操作系统，它需要系统中运行的应用程序都必须是相互独立的，各自运行在自己的Dalvik VM实例中。在正常情况下，Android应用之间是不能进行实时的数据交换，而考虑到有些应用的数据需要对外进行共享，Android系统提供了一个标准的数据接口ContentProvider，通过应用提供的ContentProvider，可以在其它应用中对这个应用的暴露出来的数据进行增删改查。
为应用程序暴露数据接口非常的简单，只需要继承ContentProvider类，并且实现insert()、delete()、update()、query()等方法，使外部应用可对本应用的数据进行增删改查。

## 意图（Intent）

虽然Intent并不是Android应用的组件，也无需专门在清单文件中配置，但是它对于Android应用的作用非常的大。除了ContentProvider之外，其它组件的启动，均需要通过Intent进行指定。Intent不仅可以明确指定一个Android组件进行启动，还可以提供一个标准的行为，再由Android系统配合意图过滤器来选定启动指定组件来完成任务。而Intent在开启对组件的过程中，进行各个组件间数据的传递。

## 小结

本章简要介绍了Android系统的发展史及其现状，并且介绍了Android系统的架构与Dalvik VM虚拟机，最后还简单介绍了Android开发中的四大组件。通过阅读本章，对Android的历史与现状、系统架构、基本组件有个大致的了解，这对本书接下来的内容理解非常有帮助。