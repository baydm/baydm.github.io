---
title: MySql常用信息函数
author: JsonYe
tags:
  - mysql
  - 数据库
categories:
  - MySql 
copyright: true
comments: true
toc: true
date: 2017-01-12 16:59:00
---
## 基本命令
```sql
-- 管理员登录
mysql -uroot
-- 查看当前服务器版本
select version();
-- 查看当前使用的数据库
select database();
-- 当前用户
select current_user();
select user();

-- 查询当前日期、时间、日期+时间
select curdate(),curtime(),now();
select current_date(),current_time(),current_timestamp();

-- 显示所有表
show tables;
-- 显示所有库
show databases;
-- 查看标准建库语句
show create database db_name;
-- 查看标准建表语句
show create table tb_name;
-- 查看表字段信息
show full columns from tname;
-- 显示当前数据库服务器支持的存储引擎
show engines;
-- 查询当前服务器所支持的字符集。
show charset;

```

## 存储引擎
- MyISAM 不支持事务，速度快，引用最多的引擎
- InnoDB 支持事务

## 常见支持简体中文的字符集
我国定制，支持中文简体、繁体 日文。
gb2312 简体中文，只支持6763简体汉字
gbk 简繁体支持
gb18030 

utf-8 美国制定，支持所有国家语言