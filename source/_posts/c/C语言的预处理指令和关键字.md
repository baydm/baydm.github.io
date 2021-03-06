---
title: C语言的预处理指令和关键字
author: JsonYe
tags:
- c
categories:
- C语言
copyright: true
comments: true
toc: true
date: 2015-12-20 21:24:00   
---
## 预处理指令
- C语言在对源程序进行编译之前，会先对一些特殊的预处理指令作解释，产生一个新的源程序(这个过程称为编译预处理),之后再进行通常的编译
- 为了区分预处理指令和一般的C语句，所有预处理指令都以符号“#”开头，并且结尾不用分号
- 预处理指令可以出现在程序的任何位置，它的作用范围是从它出现的位置到文件尾。习惯上我们尽可能将预处理指令写在源程序开头，这种情况下，它的作用范围就是整个源程序文件
- C语言提供的预处理指令主要有：宏定义、文件包含、条件编译

### 定义
宏定义可以分为2种：

1. 不带参数的宏定义 
    - 定义格式：
    ```
    #define 宏名 字符串
    // 比如  #define ABC 10
    ```
    - 作用：是在编译预处理时，将源程序中所有"宏名"替换成右边的"字符串"，常用来定义常量。
    - 使用习惯与注意
        1. 宏名一般用大写字母，以便与变量名区别开来，但用小写也没有语法错误
        2. 对程序中用双引号扩起来的字符串内的字符，不进行宏的替换操作。
        3. 在编译预处理用字符串替换宏名时，不作语法检查，只是简单的字符串替换。只有在编译的时候才对已经展开宏名的源程序进行语法检查
        4. 宏名的有效范围是从定义位置到文件结束。如果需要终止宏定义的作用域，可以用#undef命令
        5. 定义一个宏时可以引用已经定义的宏名
    
2. 带参数的宏定义
    - 定义格式：
    ```
    #define 宏名(参数列表) 字符串
    ```
    - 作用：在编译预处理时，将源程序中所有宏名替换成字符串，并且将 字符串中的参数 用 宏名右边参数列表 中的参数替换.
    - 使用注意：
        1. 宏名和参数列表之间不能有空格，否则空格后面的所有字符串都作为替换的字符串.
        2. 带参数的宏在展开时，只作简单的字符和参数的替换，不进行任何计算操作。所以在定义宏时，一般用一个小括号括住字符串的参数。
        3. 参数和计算结果都要用小括号括起来
    - 与函数的区别：从整个使用过程可以发现，带参数的宏定义，在源程序中出现的形式与函数很像。但是两者是有本质区别的：
        1. 宏定义不涉及存储空间的分配、参数类型匹配、参数传递、返回值问题
        2. 函数调用在程序运行时执行，而宏替换只在编译预处理阶段进行。所以带参数的宏比函数具有更高的执行效率
        
### 条件编译
>在很多情况下，我们希望程序的其中一部分代码只有在满足一定条件时才进行编译，否则不参与编译(只有参与编译的代码最终才能被执行)，这就是条件编译。
 
- 格式  
```   
#if 条件1
  ...code1...
#elif 条件2
  ...code2...
#else
  ...code3...
#endif
```

- 注意
>条件编译结束后，要在最后面加一个#endif，不然后果很严重。
`#if` 和 `#elif`后面的条件一般是判断宏定义而不是判断变量，因为条件编译是在编译之前做的判断，宏定义也是编译之前定义的，而变量是在运行时才产生的、才有使用的意义。

- 条件编译其它用法
```
#if defined()和#if !defined()的用法
//#if defined(MAX)
#if !defined(MAX)
    ...code...
#endif
#ifdef 和 ifndef的用法
 //#ifdef MAX
 #ifndef MAX
     ...code...
 #endif
```
## static/extern
### static和extern关键字对函数的作用
- 外部函数和内部函数
    - 外部函数：如果在当前文件中定义的函数允许其他文件访问、调用，就称为外部函数。C语言规定，不允许有同名的外部函数。
    - 内部函数：如果在当前文件中定义的函数不允许其他文件访问、调用，只能在内部使用，就称为内部函数。C语言规定不同的源文件可以有同名的内部函数，并且互不干扰。
- `extern`
    - 在定义函数时，如果在函数的最左边加上关键字extern，则表示此函数是外部函数，可供其他文件调用。C语言规定，如果在定义函数时省略extern，则隐含为外部函数。
    - 在一个文件中要调用其他文件中的外部函数，则需要在当前文件中用extern声明该外部函数，然后就可以使用，这里的extern也可以省略。
- `static`
    - 在定义函数时，在函数的最左边加上static可以把该函数声明为内部函数(又叫静态函数)，这样该函数就只能在其定义所在的文件中使用。如果在不同的文件中有同名的内部函数，则互不干扰。
    - static也可以用来声明一个内部函数

### static和extern关键字对全局变量的作用
1. extern可以用来声明一个全局变量，但是不能用来定义变量
2. 默认情况下，一个全局变量是可以供多个源文件共享的，也就说，多个源文件中同名的全局变量都代表着同一个变量
3. 如果在定义全局变量的时候加上static关键字，此时static的作用在于限制该全局变量的作用域，只能在定义该全局变量的文件中才能使用，跟其他源文件中的同名变量互不干扰

### Static对局部变量的作用
1. 用static修饰局部变量后会延长局部变量的生命周期，当执行到定义变量的那一行的时候分配存储空间，但是直到程序结束变量才会释放
2. 尽管延长了变量的生命周期，但是没有改变变量的作用域
    使用场合：当一个变量要被经常重复使用的时候就可以用static来修饰这个变量

## typedef
>可以使用typedef关键字为各种数据类型定义一个新名字(别名)，可以简化代码和提高阅读性。

### typedef与指针
```
typedef char *String;
int main(int argc, const char * argv[]) {
    // 相当于char *str = "This is a string!";
    String str = "This is a string!";    
    printf("%s", str);   
    return 0;
 }
```

### typedef与结构体
```
// 定义一个结构体
struct MyPoint {
    float x;
     float y;
}; 
int main(int argc, const char * argv[]) {
   // 定义结构体变量
    struct MyPoint p;
    p.x = 10.0f;
    p.y = 20.0f;
    retuen 0;    
}
```
### 使用typedef给结构体起别名
```
// 定义一个结构体
struct MyPoint {
   float x;
   float y;
};
// 起别名
typedef struct MyPoint Point; 
int main(int argc, const char * argv[]) {
  // 定义结构体变量
  Point p;
  p.x = 10.0f;
  p.y = 20.0f;    
  return 0;
}
```
### typedef与指向结构体的指针
```
// 定义一个结构体并起别名
 typedef struct {
    float x;
    float y;
 } Point; 
 // 起别名
 typedef Point *PP; 
 int main(int argc, const char * argv[]) {
    // 定义结构体变量
    Point point = {10, 20};    
    // 定义指针变量
    PP p = &point;     
    // 利用指针变量访问结构体成员
    printf("x=%f，y=%f", p->x, p->y);
    return 0;
}
```
### typedef与指向函数的指针
```
// 定义一个sum函数，计算a跟b的和
  int sum(int a, int b) {
      int c = a + b;
      printf("%d + %d = %d", a, b, c);
      return c;
  }  
 typedef int (*MySum)(int, int);
 int main(int argc, const char * argv[]) {
     // 定义一个指向sum函数的指针变量p
     // int (*p)(int, int) = sum;  
     // 定义一个指向sum函数的指针变量p
     MySum p = sum;   
     // 利用指针变量p调用sum函数
     (*p)(4, 5);
     return 0;
 }
```
### typedef与#define
```
typedef char *String1;//其别名
#define String2 char *//宏定义，在代码中只是将(char *)替换称String
int main(int argc, const char * argv[]) 
    String1 str1, str2;   // 实际是char *str1,char *str2
    String2 str3, str4;   // 实际是char *str3,char str4
    return 0;
}
```

### 使用场合：
 - 给基本数据类型起别名
 - 给指针起别名
 - 给结构体起别名
 - 给枚举起别名
 - 给指向函数的指针起别名
 - 给指向结构体的指针起别名