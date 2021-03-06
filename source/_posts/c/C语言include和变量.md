---
title: C语言include和变量
author: JsonYe
tags:
- c
categories:
- C语言
copyright: true
comments: true
toc: true
date: 2015-12-19 23:24:00   
---
## 常见函数

- main函数
main函数时整个C程序的入口，整个C程序中也有且仅有一个main函数
- printf函数
在屏幕上输出内容，使用前必须加 `#incluce <stdio.h>`

## `#include`
- `#include`指令介绍
    - `#include` 是C语言的`预处理指令`之一。    
    在编译之前做的处理，预处理指令一般以`#`开头    
    - `#include`指令后面会跟着一个文件名，此时，会将该文件内容包含到当前文件中。
    - 如果本包含的文件拓展名为 `.h` 则称为头文件(Header File)。
    - `#include`指令不仅限于 `.h` 头文件，可以包含任何白安逸器能识别的C/C++代码文件 
- `#include <>`和`#include ""`区别（主要是检索顺序不同）
    - `#include <>` 检索顺序：
    父文件所在文件夹 → 父文件的父文件所在文件夹 → 编译器设置的include路径 → 系统INCLUDE环境变量
    - `#include " "` 检索顺序：
    编译器设置的include路径 → 系统INCLUDE环境变量
- `stdio.h`
    - 是C语言函数库中的一个头文件

## 多源文件开发

1. 在编写第一个C程序的时候已经提到：我们编写的所有C语言代码都保存在拓展名为.c的源文件中，编写完毕后就进行编译、链接，最后运行程序。
2. 在实际开发过程中，项目做大了，源代码肯定非常多，很容易就上万行 代码了，甚至上十万、百万都有可能。这个时候如果把所有的代码都写到一个.c源文件中，那么这个文件将会非常庞大，也非常恶心，你可以想象一下，一个文件 有十几万行文字，不要说调试程序了，连阅读代码都非常困难。
3. 公司里面都是以团队开发为主，如果多个开发人员同时修改一个源文件，那就会带来很多麻烦的问题，比如张三修改的代码很有可能会抹掉李四之前添加的代码。
4. 因此，为了模块化开发，一般会将不同的功能写到不同的.c源文件中，这样的话，每个开发人员都负责修改不同的源文件，达到分工合作的目的，能够大大提高开发效率。也就是说，一个正常的C语言项目是由多个.c源文件构成。

----

## 常用UNIX指令
| 指令 | 作用|
| :--- | :----|
| ls | 列出当前目录下的所有内容（文件\文件夹）|
| pwd | 显示出当前目录的名称|
| cd | 改变当前操作的目录|
| who | 显示当前用户名|
| clear | 清除所有内容|
| mkdir | 创建一个新目录|

## 编译C程序
- 编译one.c，生成one.o文件
```cc -c one.c```

- 链接one.o，生成a.out文件
```cc one.o```

- 运行a.out
```./a.out```

## 进制
    进制：一种计数方式
- 十进制
由0、1、2….9十个基本数字组成；运算规则是“逢十进一”
- 二进制
特点：由0、1两个基本数字组成；运算规则是“逢二进一”
书写形式：需要以0b或者0B开头，比如0b101
- 八进制
特点：由0~7八个基本数字组成；运算规则是“逢八进一”
书写形式：在前面加个0，比如045
- 十六进制
特点：由0~9和A~F组成，A~F分别表示10~15；运算规则是“逢十六进一”
书写形式：在前面加个0x或者0X，比如0x45

## 位运算符
运算符 | 作用  | 说明 |举例
 -----|-------|----|---
&| 按位与|只有对应的两个二进位均为1时，结果位才为1，否则为0|1001 & 0101 = 0001
&#x7c;| 按位或|只要对应的二个二进位有一个为1时，结果位就为1，否则为0|1001 &#x7c; 0101 = 1101
^ |按位异或|当对应的二进位相异（不相同）时，结果为1，否则为0|1001 ^ 101 = 1100
~ |取反|各二进位进行取反（0变1，1变0）|~1001 = 0110
<< |左移|各二进位全部左移n位，高位丢弃，低位补0|乘以2的n次方
&#x3e;&#x3e; |右移|各二进位全部右移n位，保持符号位不变|是除以2的n次方    
```
//使用位运算实现交换两个数的值
a = a^b;
b = b^a;
a = a^b;
```
## 变量的内存分析
### 字节和地址
- 内存以“字节为单位”，不同类型的变量在不同编译器环境下所占的空间也不同

变量类型 | 16位编译器  | 32位编译器  | 64位编译器
--|--|--|--
char |1|1|1
int |2|4|4
float|4|4|4
double|8|8|8
- 变量存储单元的第一个字节的地址就是该变量的地址
- 负数的二进制形式，就是对它的正数的二进制取反后加1

## 类型说明符
类型|说明|64位编译器
--|--|--
short|短型|2字节（16位）
long|长型|8字节（64位）
signed|有符号型
unsigned|无符号型
>一般就是用来修饰int类型的，所以在使用时省略int。
short int等价于short，long int等价于long，long long int等价于long long

- signed和unsigned的区别就是它们的最高位是否要当做符号位，并不会像short和long那样改变数据的长度，即所占的字节数。
- signed：表示有符号，也就是说最高位要当做符号位，所以包括正数、负数和0。其实int的最高位本来就是符号位，已经包括了正负数和0了，因此signed和int是一样的，signed等价于signed int，也等价于int。signed的取值范围是<img src="http://www.forkosh.com/mathtex.cgi? -2^{31}"> ~ <img src="http://www.forkosh.com/mathtex.cgi? 2^{31}-1">
- unsigned：表示无符号，也就是说最高位并不当做符号位，所 以不包括负数。在64bit编译器环境下面，int占用4个字节（32bit），因此unsigned的取值范围是：0000 0000 0000 0000 0000 0000 0000 0000 ~ 1111 1111 1111 1111 1111 1111 1111 1111，也就是0~<img src="http://www.forkosh.com/mathtex.cgi? 2{32}-1">

## char类型（字符型）
- 一个字符型变量占用1个字节，共8位。范围是<img src="http://www.forkosh.com/mathtex.cgi? -2^7">~<img src="http://www.forkosh.com/mathtex.cgi? 2^7-1">。
- 不能用来存储汉字
- 前面加"\"形成的字符，称为“转义字符”  

转义字符|意义|ASCII码值
--|--|--
\n|回车|10
\t|退格|9
\\|\|92
\'|'|39
\"|"|34
\0|空字符|0



