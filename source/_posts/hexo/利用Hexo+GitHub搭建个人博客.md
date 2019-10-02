title: 利用Hexo+GitHub搭建个人博客(一)
categories:
  - hexo
tags:
  - hexo
author: JsonYe
date: 2019-09-30 13:55:00
---

## 前言
很久以前的一个想法，就是搭建一个个人博客，把个人在学习、生活中的故事记录下来。`hexo`让我的想法变成了现实。
下面就简单说一下整体打搭建流程。

## 搭建步骤：
> 最开始以为要把hexo安装到服务器上，后来了解后恍然大悟，他是在本地安装的，然后将我们写的markdown文件转换为静态网站文件，放到github上，利用github来作为服务器的。

 1. 安装git bash。
 2. 安装npm。
 3. 安装NodeJs
 4. 申请github账户，并创建一个仓库，命名规范为  "账户名".github.io。
 5. 创建SSH并添加到github上。
 6. 安装hexo。
 7. 部署项目，本地测试。
 8. 上传到github上。
 
到这一步，博客就搭建好了，域名可选择性进行关联。后续可以设置主题、添加RSS、设置评论、以及写文章。具体可参考[官方文档](https://hexo.io/zh-cn/docs/writing.html)