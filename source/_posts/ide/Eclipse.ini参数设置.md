title: Eclipse.ini参数设置
author: JsonYe
tags:
  - eclipse
categories:
  - IDE  
copyright: true
comments: true
toc: true
date: 2015-04-16 14:03:00
---
### vmargs下常见参数的意思：
```
-vmargs  
-Xms40m  
-Xmx256m  
-XX:PermSize=64M  
-XX:MaxPermSize=128M
```

- -vmargs: 说明后面是VM的参数  
- -Xms40m: 虚拟机占用系统的最小内存,初始分配  
- -Xmx256m: 虚拟机占用系统的最大内存,按需分配  
- -XX:PermSize: 最小堆大小。一般报内存不足时,都是说这个太小, 堆空间剩余小于5%就会警告,建议把这个稍微设大一点,不过要视自己机器内存大小来设置，但不能超过MaxPermSize  
- -XX:MaxPermSize: 最大堆大小。这个也适当大些所以若出现问题，首先请调整 `-Xms40m：`将其设置的小一些，就可以解决问题`PermSize`和`MaxPermSize`指虚拟机为java永久生成对象（Permanate generation）等这些可反射对象分配内 存的限制，这些内存不包括在Heap（堆内存）区之中.

### 解决Failed to creat java virtual machine问题:  
打开eclipse安装目录下的eclipse.ini文件，修改：  
```
--launcher.XXMaxPermSize  
128M;  
```
为：
```  
--launcher.XXMaxPermSize  
256m
```
设置Eclipse使用的JRE为本机安装的JDK目录：  
在eclipse.ini中添加两行  
```
 -vm  
C:\\Program Files\\Java\\jdk1.6.0_10\\bin\\javaw.exe   
```
* 注意: 要写在两行，写在一行不能生效；这两行要定在-vmargs之前，不然也不能生效。

### 我的eclipes.ini文件配置如下：

```
-startup
plugins/org.eclipse.equinox.launcher_1.3.0.v20140415-2008.jar
--launcher.library
plugins/org.eclipse.equinox.launcher.win32.win32.x86_64_1.1.200.v20140603-1326
-product
org.eclipse.epp.package.java.product
-showsplash
org.eclipse.platform
--launcher.defaultAction
openFile
--launcher.XXMaxPermSize
384M
-vm
C:\Program Files\Java\jre7\bin\javaw.exe
-vmargs
-Dcom.sun.management.jmxremote 
-Dosgi.requiredJavaVersion=1.6
-Xverify:none
-Xmn128m
-Xms256m
-Xmx768m
-Xss1m
-XX:PermSize=128M
-XX:MaxPermSize=512M
```