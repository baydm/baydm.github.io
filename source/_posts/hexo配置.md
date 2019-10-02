title: 利用Hexo+GitHub搭建个人博客(二)
categories:
  - hexo
tags:
  - hexo
author: JsonYe
date: 2019-09-30 14:55:00
---
> 安装好hexo后，可进行各项配置

### 关于页面
使用：`hexo new page “about” `新建一个 关于我 页面。 
主题的` _config.yml `文件中的 `menu` 中进行匹配 
不同主题 `_config. yml`文件有区别
```
menu:
  home: /      //主页
  categories: /categories //分类
  archives: /archives   //归档
  tags: /tags   //标签
  about: /about   //关于                  （添加此行即可）
或    
menu:
  - page: home
    directory: .      //主页
    icon: fa-home
  - page: archive
    directory: archives/    //归档
    icon: fa-archive
  - page: about
    directory: about/    //关于
    icon: fa-user
  - page: rss
    directory: atom.xml    //rss订阅
    icon: fa-rss
```
编辑 about 关于页面 md文件 部署就能看到

### 添加分类
使用： `hexo new page categories` 新建一个 分类 页面。  
主题的 `_config.yml` 文件中的 `menu` 中进行匹配
```
menu:
  home: /      //主页
  categories: /categories //分类   
  archives: /archives   //归档
  tags: /tags   //标签                  
  about: /about   //关于
```
底下代码是一篇包含 分类 文章的例子：
```
title: 分类测试
categories:
- hexo                       （这个就是文章的分类了）
```


### 添加RSS
#### 安装
hexo博客有一个专门生成RSS xml文件的插件`hexo-generator-feed`
我们来安装它
```
npm install hexo-generator-feed
```

看到`added 3 packages`说明安装成功了。

#### 启用
在博客工程文件根目录下`_config.yml`文件中添加如下内容
```
# Extensions
plugins:
    hexo-generator-feed
#Feed Atom
feed:
    type: atom
    path: atom.xml
    limit: 20
```

#### 生成RSS
```
$ hexo g
(node:6520) [DEP0061] DeprecationWarning: fs.SyncWriteStream is depre                                                                                                                           cated.
INFO  Start processing
INFO  Files loaded in 6.33 s
INFO  Generated: atom.xml <----------成功生成atom.xml文件
INFO  Generated: sitemap.xml
INFO  Generated: baidusitemap.xml
INFO  Generated: about/index.html
......
......
......
```