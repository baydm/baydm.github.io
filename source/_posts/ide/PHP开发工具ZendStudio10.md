---
title: PHP开发工具ZendStudio10
author: JsonYe
tags:
  - php
categories:
  - IDE 
copyright: true
comments: true
toc: true
date: 2015-04-17 16:59:00
---
## 一、zend studio 10破解/汉化，参考文档

[http://blog.csdn.net/qq1355541448/article/details/16807429](http://blog.csdn.net/qq1355541448/article/details/16807429)

## 二、安装Composer

去到官网下载[https://getcomposer.org/download/](https://getcomposer.org/download/)

[![image](http://static.oschina.net/uploads/img/201504/17120800_gpew.png "image")](http://static.oschina.net/uploads/img/201504/17120759_Znd7.png)

## 常见问题
### windows下Composer因php_openssl扩展缺失而安装失败。

Composer( https://getcomposer.org/ )是PHP下的一个依赖管理工具。你可以在你的项目中声明你所需要用到的类库，然后Composer会在项目中为你安装它们。如果你了解Node的 npm 或者Ruby的 Bundler ，就理解它是做什么的了，但是，它不是包管理器。

在Windows的Wamp环境下安装Composer(注：Composer要求PHP版本在5.3.2+)，你可能会遇到这种安装失败的情况：出错信息是


```
 "The openssl extension is missing, which will reduce the security and stability of Composer. If possible you should enable it or recompile php with --with-openssl" ，大意就是你的PHP缺少openssl扩展。

你可能会去屏幕右下角的Wamp的控制台，去加载php的openssl扩展，或者在php.ini中去掉 extension=php_openssl.dll 这一行开头的注释，然后重启server，结果发现还是不行。

正确的做法是在php的安装目录比如说C:\wamp\bin\php\php5.3.3\中，找到找个目录下的php.ini文件，然后去掉 extension=php_openssl.dll 这一行开头的注释，之后就可以顺利安装Composer了。

你可以发现上面出现了两个php.ini，是的Wamp在Apache和在CLI(命令行)模式下使用了不同的php.ini文件，当你在WAMP的控制台去启用php_openssl这个扩展，是启用的Apache的，而非CLI。而修改php安装目录中的php.ini配置文件，则可以启用CLI模式下的openssl。
```

### Win7下运行php Composer出现SSL报错的问题没有安装CA证书导致的！！！[http://my.oschina.net/yearnfar/blog/346727](http://my.oschina.net/yearnfar/blog/346727)

CA证书下载地址：http://curl.haxx.se/docs/caextract.html

然后修改php.ini文件

```
openssl.cafile= D:/wamp/php/verify/cacert.pem
```