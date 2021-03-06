---
title: C语言表达式和结构控制
author: JsonYe
tags:
- c
categories:
- C语言
copyright: true
comments: true
toc: true
date: 2015-12-19 17:24:00   
---
# 输入输出
## printf和scanf的使用
### printf和scanf输出输入格式
| Type      | Example 
| :--:      | :-----: 
| char      | %c
| short int | %hd
| int       | %d
| long int  | %ld
| float     | %f
| double    | %f

# 表达式
## 算数运算符
### 常见运算符
运算符 | 意义
-|:--
+|加法运算符
-|减法运算符，或者负数云算法
*|乘法运算符
/|除法运算符（整数相除，省略小数）
%|模运算符，取余运算符（%两侧均为整数）
### 运算循序
1> 算术表达式:用算术运算符将数据连接起来的式子，例如 2 + 4，3 `*` 5等。
    表达式的运算顺序是按照运算符的`结合方向`和`优先级`进行的。
2> 结合方向
    算术运算符的结合方向从左到右。
3> 优先级
    优先级越高，就越先计算，当优先级相同时，参考结合方向。下面是优先级的排序
    负值运算符(-) > 乘(*)、除(/)、模(%) > 加(+)、减(-)
4> 小括号
    如果被()括起来，那么优先级是最高。
### 注意点
1. 自动类型转换， 自动将大类型转换称小类型，会丢失精度    
2. 强制类型转换

## 赋值运算符
1. 简单赋值运算符
    赋值运算符的结合方向：从右到左，而且优先级低于算数运算符
2. 复合赋值运算符
    += : 如 a+=2等价于，a = a+2;
    -= : 如 a-=2等价于，a = a-2;
   `*`= : 如 a`*`=2等价于，a = a`*`2;
    /= : 如 a+=2等价于，a = a+2;
    %= : 如 a+=2等价于，a = a+2;

## 自增和自减
1. ++
    - 先加，后用 `++a`
    - 先用，后加 `a++`
2. --
    - 先减，后用 `--a`
    - 先用，后减 `a--`
    
## sizeof
>用来计算一个变量或者一个常量、一种数据类型所占的内存字节数

## 逗号运算符
- 主要用于连接表达式
- 从左到右依次计算
- 整个都好运算符，是最后一个表达式的值

## 关系运算符
- C语言中条件成立成为“真”，条件不成立成为“假”
- C语言中规定，任何数值都有真假性，任何非0的值都为“真”，只有0才为“假”
### 关系运算符

运算符 | 意义
-|-
<|小于
<=|小于等于
>|大于
>=|大于等于
==|等于
！=|不等于

关系运算符的结果只有两种，条件成立结果是“1”，不成立为“0”；
### 优先级
1. <、<=、>、>=优先级大于 ==、!=优先级
2. 结合方向，“从左到右”
3. 优先级低于算术运算符

## 逻辑运算符

运算符|意义|计算规则
-|- | -
&&|与|两个为真才为真
&#124;&#124; | 或|一个为真就为真
！ | 非|！真为假，！假为真

## 三目运算符
- 条件运算符
> 表达式1？表达式2：表达式3;
    表达式1为真，执行表达式2，反之执行表达式3

# 控制结构
## 3种流程控制结构
- 顺序结构：默认的流程结构。
- 选择结构：对给定的条件进行判断，再根据判断来决定执行哪一段代码。
- 循环结构：在给定条件成立的情况下，反复执行莫一段代码。

### 选择结构
1. if(){}else{}
2. switch(){case :}

### 循环结构
1. while
```
while(条件）｛
    语句1；
    ……
}
//条件成立（为真），就执行{}中内容，条件不成立，就不执行
```

2. do-while
```
do{
    语句1；
}while(条件);
// 先执行一遍{}中内容，再判断'条件'是否成立，成立继续执行，不成立，不执行。
```

3. for
```
/*
执行循序：
1.初始化表达式（只在开始的时候执行一次）
2.循环条件表达式（返回值只有两种，真 或 假）
3.2返回为真时，执行{}中内容。为假时，退出循环
4.执行一次{}后，执行“循环后的操作表达式”
5.再执行第2步，循环下去。
*/
for(初始化表达式；循环条件表达式；循环后的操作表达式){
    执行语句；
}
```
- break和continue
    break常使用与switch和循环结构中，用于跳出switch或循环
    continue常用于循环结构中，用于跳出本次循环