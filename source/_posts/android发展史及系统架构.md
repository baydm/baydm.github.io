title: android发展史及系统架构
author: JsonYe
tags:
  - Android
categories:
  - Android基础
copyright: true
date: 2015-04-29 17:32:00
---

## 1.1 Android发展史与现状

Andy Rubin创立22个月后→（2005年）Google收购。

2008 Patrick Brady于Google I/O 演讲“Anatomy & Physiology of an Android”，并提出的 Android HAL 架构图。

### Android版本升级  
Android系统今后将继续每半年一次的升级步伐，分别定在每年的夏天和年终。每代Android系统都将以食物命名，比如1.5版叫做 Cupcake(纸杯蛋糕)，1.6版为Donut(甜甜圈)，然后是Eclair(法式奶油夹心甜点)和Flan(水果馅饼)。Donut将把社交网络功能作为升级重点，在“手机的各种体验中”都增加社交网络元素。  
#### 1.5 (Cupcake)  
基于Linux Kernel 2.6.27 2009年4月30日，官方1.5版本(Cupcake)的Android发布。主要的更新如下:  
● 拍摄/回放视频，并支持上传到youtube  
● 支持立体声蓝牙耳机，同时改善自动配对性能  
● 最新的采用WebKit技术的浏览器，支持拷贝/粘帖和页面中搜索  
● GPS性能大大提高  
● 屏幕虚拟键盘  
● 主屏幕增加音乐播放器和相框widgets  
● 应用程序自动随着手机旋转  
● 短信，Gmail，日历，浏览器的用户界面大幅改善，比如说Gmail现在可以批量删除邮件了  
● 相机启动速度加快，拍摄图片可以直接上传到picasa  
● 来电照片显示  
#### 1.6 (Donut)  
基于Linux Kernel 2.6.29 2009年9月15日, 1.6(Donut)版本SDK发布。主要的更新如下:  
● 完全重新设计的Android Market  
● 手势支持  
● 支持CDMA网络  
● 文字转语音系统(TXT-2-speech)  
● 快速搜索框  
● 全新的拍照界面  
● 应用程序耗电查看  
● 支持VPN  
● 支持更多的屏幕分辨率  
● 支持OpenCore2媒体引擎  
● 新增面向视觉或听觉困难人群的易用性插件  
#### 2.0/2.0.1/2.1(Eclair)  
基于Linux Kernel 2.6.29 2009年10月26日, 2.0(Eclair)版本SDK发布。主要的更新如下:  
● 优化硬件速度  
● "Car Home"程序  
● 支持更多的屏幕分辨率  
● 重整界面  
● 新的浏览器的用户界面和支持HTML5  
● 新的联系人名单  
● 更好的白色/黑色背景比率  
● 改进Google Maps 3.1.2  
● 支持Microsoft Exchange  
● 支持内置相机闪光灯  
● 数字变焦  
● 改进的虚拟键盘  
● 蓝牙2.1  
Android的代号序列会按甜点名字中首个英文字母(C、D、E、F)的排列顺序。  
下一个版本的Android将会命名为Froyo(冻酸奶,基于Linux Kernel 2.6.32)。Froyo 之后的版本的Android将会命名为Gingerbread(姜饼,基于Linux Kernel 2.6.33/34)。

**Android****版本**

**发布日期**

**代号**

**Android 1.1**

**Android 1.5**

2009年4月30日

Cupcake（纸杯蛋糕）

**Android 1.6**

2009年9月15日

Donut（炸面圈）

**Android 2.0/2.1**

2009年10月26日

Eclair（长松饼）

**Android 2.2**

2010年5月20日

Froyo（冻酸奶）

**Android 2.3**

2010年12月6日

Gingerbread（姜饼）

**Android 3.0/3.1/3.2**

2011年2月22日

Honeycomb（蜂巢）

**Android 4.0**

2011年10月19日

Ice Cream Sandwich（冰淇淋三明治）

**Android 4.1**

2012年6月28日

Jelly Bean（果冻豆）

**Android 4.2**

2012年10月8日

Jelly Bean（果冻豆）

**Android5.0**

待定

Lime Pie（酸橙派）

### 1.2 Android系统的架构与特性

#### 1.2.1 Android系统架构

Android系统的底层是建立在Linux系统之上的，它采用软件叠层（Software Stack）的方式进行构建。使得层与层之间相互分离，明确各层的分工。这种分工保证了层与层之间的低苟合，当下层发生改变的时候，上层应用程序无需做任何改变。

下图为Android系统的系统架构图：

![](http://s1.51cto.com/wyfs02/M01/25/73/wKioL1NgW-Si7ae7AAEJ_vZkaJ0908.jpg)

如图可知，Android系统分为四个层，从高到底分别是：应用程序层（Application）、应用程序框架层（Application Framework）、系统运行库层（Libraries）和Linux内核层（Linux Kernel）。

Android操作系统可以在四个主要层面上分为5个部分：

##### 1\. 应用程序层（Application）

Android系统包含了一系列核心应用程序，包括电子邮件、短信SMS、日历、拨号器、地图、浏览器、联系人等。这些应用程序都是用Java语言编写。本书重点讲解如何编写Android系统上运行的应用程序，在程序分层上，与系统核心应用程序平级。

##### 2\. 应用程序框架层（Application Framework）

Android应用程序框架提供了大量的API供开发人员使用，Android应用程序的开发，就是调用这些API，根据需求实现功能。

应用程序框架是应用程序的基础。为了软件的复用，任何一个应用程序都可以开发Android系统的功能模块，只要发布的时候遵循应用程序框架的规范，其它应用程序也可以使用这个功能模块。

##### 3\. 系统运行库层（Libraries）**

Android系统运行库是用C/C++语言编写的，是一套被不同组件所使用的函数库组成的集合。一般来说，Android应用开发者无法直接调用这套函数库，都是通过它上层的应用程序框架提供的API来对这些函数库进行调用。

下面对一些核心库进行简单的介绍：

> **Libc：**从BSD系统派生出来的标准C系统库，在此基础之上，为了便携式Linux系统专门进行了调整。
> 
> **Medio Framework：**基于PacketView的OpenCORE，这套媒体库支持播放与录制硬盘及视频格式的文件，并能查看静态图片。
> 
> **Surface Manager：**在执行多个应用程序的时，负责管理显示与存取操作间的互动，同时负责2D绘图与3D绘图进行显示合成。
> 
> **WebKit：**Web浏览器引擎，该引擎为Android浏览器提供支持。
> 
> **SGL：**底层的2D图像引擎。
> 
> **3D libraries：**基于OpenGL ES 1.0API，提供使用软硬件实现3D加速的功能。
> 
> **FreeType：**提供位图和向量字体的支持。
> 
> **SQLite：**轻量级的关系型数据库。


##### 4\. Android运行时**

    Android运行时由两部分完成：Android核心库和Dalvik虚拟机。其中核心库集提供了Java语言核心库所能使用的绝大部分功能，Dalvik虚拟机负责运行Android应用程序。

    虽然Android应用程序通过Java语言编写，而每个Java程序都会在Java虚拟机JVM内运行，但是Android系统毕竟是运行在移动设备上的，由于硬件的限制， Android应用程序并不使用Java的虚拟机JVM来运行程序，而是使用自己独立的虚拟机Dalvik VM，它针对多个同时高效运行的虚拟机进行了优化。每个Android应用程序都运行在单独的一个Dalvik虚拟机内，因此Android系统可以方便对应用程序进行隔离。

##### 5\. Linux内核

Android系统是基于Linux2.6之上建立的操作系统，它的Linux内核为Android系统提供了安全性、内存管理、进程管理、网络协议栈、驱动模型等核心系统服务。Linux内核帮助Android系统实现了底层硬件与上层软件之间的抽象。

#### 1.2.2 Dalvik VM和JVM的区别

JVM（Java虚拟机）是一个虚构出来的运行Java程序的运行时，是通过在实际的计算机上仿真模拟各种计算机功能的实现。它具有完善的硬件架构（如处理器、堆栈、寄存器等），还具有相应的指令系统，使用JVM就是使Java程序支持与操作系统无关。理论上在任何操作系统中，只要有对应的JVM，即可运行Java程序。

Dalvik VM是在Android系统上运行Android程序的虚拟机，其指令集是基于寄存器架构的，执行特有的文件格式-dex字节码来完成对象生命周期管理、堆栈管理、线程管理、安全异常管理、垃圾回收等重要功能。

由于Android应用程序的开发编程语言是Java，而Java程序运行在JVM（Java虚拟机）上的，因此有些人会把Android的虚拟机DalvikVM和JVM弄混淆，但是实际上Dalvik并未遵守JVM规范，而且两者也是互不兼容。

从Dalvik VM和JVM的编译过程分析，它们的编译过程如下：

```
JVM：.java→.class→.jar
Dalvik VM：.java→.class→.dex
```

从它们的编译过程可以看出，JVM运行的是.class文件的Java字节码，但是Dalvik VM运行的是其转换后的dex（Dalvik Executable）文件。JVM字节从.class文件或者JAR包中加载字节码然后运行，而Dalvik VM无法直接从.class文件或JAR包中加载字节码，它需要通过DX工具将应用程序所有的.class文件编译成一个.dex文件，Dalvik VM则运行这个.dex文件。

下图显示了Dalvik VM与JVM编译过程的区别：

![](http://s4.51cto.com/wyfs02/M01/25/73/wKiom1NgXMOTVyNiAAB-h8_94xE986.jpg)

从图中可以看出，Dalvik VM把.java文件编译成.class后，会对.class进行重构，整合的基本元素（常量池、类定义、数据段）,最后压缩写进一个.dex文件中。其中，常量池描述了所有的常量，包括引用、方法名、数值常量等；类定义包括访问标识、类名等基本信息；数据段中包含各种被VM指定的方法代码以及类和方法的相关信息和实例变量。这种把多个.class文件进行整合的方法，大大提高了Android程序的运行速度，例如：应用程序中多个类定义了字符串常量TAG，而在JVM中，会编译成多个.class文件，每个.class文件的常量池中，均包含这个TAG常量，但是Dalvik VM在编译成.dex文件之后，其常量池里只有一个TAG常量。

JVM和Dalvik VM还有一点非常重要的不同，就是基于的架构不同。JVM是基于栈的架构，而Dalvik VM是基于寄存器的架构。相对于基于栈的JVM而言，基于寄存器的Dalvik VM实现虽然牺牲了一些硬件上的通用性，但是它在代码的执行效率上要更胜一筹。一般来讲，VM中指令的解释执行的时间主要花费在以下三个方面：

> 分发指令；
> 
> 访问运算数；
> 
> 执行运算；


其中分发指令这个环节对性能的影响最大。在基于寄存器的Dalvik VM中，可以更有效的减少冗余指令的分发，减少内存的读写访问。

从JVM和Dalvik VM的区别上来说，Dalvik VM主要是针对Android这个嵌入式操作系统的特点进行了各种优化，使其更省电、更省内存、运行效率更高，但是牺牲了一些JVM的与平台无关的特性。实际上，Dalvik VM本就是为Android设计的，无需考虑其它平台的问题。这里只是介绍了JVM和Dalvik VM的两个重要的区别，毕竟本书并不是讲解Android内核的，这里只是点明Dalvik VM的特点，读者对这部分的内容了解即可。

### 1.2.3 Android系统平台的优势

Android系统相对于其它操作系统，有如下几点优势：

#### 1. 开放性

首先就是Android系统的开放性，其开发平台允许任何移动终端厂商加入到Android联盟中来，降低了开发门槛，使其拥有更多的开发者，随着用户和应用的日益丰富，也将推进Android系统的成熟。同时，开放性有利于Android设备的普及以及市场竞争力，这样有利于消费者买到更低价位的Android设备。

#### 2. 丰富的硬件选择

同样由于Android系统的开放性，众多硬件厂商可以推出各种的搭载Android系统的设备。现如今，Android系统不仅仅只是运行在手机上，越来越多的设备开始支持Android系统，如电视、可佩戴设备、数码相机等。

#### 3. 便于开发

Google开放了Android的系统源码，提供了开发者一个自由的开发环境，不必受到各种条条框框的束缚。

#### 4. Google服务的支持

Google公司作为一个做服务的公司，它提供了如地图、邮件、搜索等服务，Android系统可以对这些服务进行无缝的结合。