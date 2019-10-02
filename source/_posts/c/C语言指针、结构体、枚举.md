---
title: C语言指正|结构体|枚举
author: JsonYe
tags:
- c
categories:
- C语言
copyright: true
comments: true
toc: true
date: 2015-12-19 17:33:00   
---
# 指针
## 概述
指针就是用来保存变量的地址的变量

- 访问
    1. 我们通过`&`来获取变量的地址。
    2. `&`这个操作符只能指向变量或者是数组。
    3. `&`是获取地址的操作符。
    4. 使用`%p`来打印地址。

- 本质
    指针是一个4字节（或是8字节）的一个int的整数。换句话说也就一个int 型的变量
- 指针变量
    1. 指针变量是用来保存地址的。
    2. 指针变量里保存的地址可以修改。
    3. 指针变量可以指向特殊的数据类型。
    4. 可以有多个指针变量里的值是相同的。

- 一级指针的简单使用
    指针访问内存可以通过`*`这个操作符去访问所指向的内存空间。

## 指针的定义和初始化
- type * identifier
    1. 没有初始化的指针，称之为野指针。
    2. 指针里面是一个随机的值。
    3. 野指针有很大的风险。
    4. 指针可以作为函数的参数和返回值。
-   
```
// 声明一个int指针
int *ptr;
// 声明一个int值
int val = 1;
// 为指针分配一个int值的引用
ptr = &val;
// 对指针进行取值，打印存储在指针地址中的内容
int deref = *ptr;
printf("%d\n", deref);
```
第2行，我们通过`*`操作符声明了一个int指针。接着我们声明了一个int变量并赋值为1。然后我们用int变量的地址初始化我们的int指针。接下来对int指针取值，用变量的内存地址初始化int指针。最终，我们打印输出变量值，内容为1。

第6行的`&val`是一个引用。在val变量声明并初始化内存之后，通过在变量名之前使用地址操作符`&`我们可以直接引用变量的内存地址。
第8行，我们再一次使用`*`操作符来对该指针取值，可直接获得指针指向的内存地址中的数据。由于指针声明的类型是int，所以取到的值是指针指向的内存地址存储的int值。

- void指针、NULL指针和未初始化指针
一个指针可以被声明为void类型，比如void *x。一个指针可以被赋值为NULL。一个指针变量声明之后但没有被赋值，叫做未初始化指针。

```
int *uninit; 
// int指针未初始化
int *nullptr = NULL; 
// 初始化为NULL
void *vptr; 
// void指针未初始化
int val = 1;
int *iptr;
int *castptr;
 
// void类型可以存储任意类型的指针或引用
iptr = &val;
vptr = iptr;
printf("iptr=%p, vptr=%p\n", iptr, vptr);
 
// 通过显示转换，我们可以把一个void指针转成
// int指针并进行取值
castptr = (int *)vptr;
printf("*castptr=%d\n", *castptr);
 
// 打印null和未初始化指针
printf("uninit=%p, nullptr=%p\n", uninit, nullptr);
// 不知道你会得到怎样的返回值，会是随机的垃圾地址吗？
// printf("*nullptr=%d\n", nullptr);
// 这里会产生一个段错误
// printf("*nullptr=%d\n", nullptr);
执行上面的代码，你会得到类似下面对应不同内存地址的输出。

iptr=0x7fff94b89c6c, vptr=0x7fff94b89c6c
*castptr=1
uninit=0x7fff94b89d50, nullptr=(nil)
```

第1行我们声明了一个未初始化int指针。所有的指针在赋值为NULL、一个引用（地址）或者另一个指针之前都是未被初始化的。第2行我们声明了一个NULL指针。第3行声明了一个void指针。第4行到第6行声明了一个int值和几个int指针。

第9行到11行，我们为int指针赋值为一个引用并把int指针赋值为void指针。void指针可以保存各种其它指针类型。大多数时候它们被用来存储数据结构。可以注意到，第11行我们打印了int和void指针的地址。它们现在指向了同样的内存地址。所有的指针都存储了内存地址。它们的类型只在取值时起作用。

第15到16行，我们把void指针转换为int指针castptr。请注意这里需要显示转换。虽然C语言并不要求显示地转换，但这样会增加代码的可读性。接着我们对castptr指针取值，值为1。

第19行非常有意思，在这里打印未初始化指针和NULL指针。值得注意的是，未初始化指针是有内存地址的，而且是一个垃圾地址。不知道这个内存地址指向的值是什么。这就是为什么不要对未初始化指针取值的原因。最好的情况是你取到的是垃圾地址接下来你需要对程序进行调试，最坏的情况则会导致程序崩溃。
>NULL指针被初始化为o。NULL是一个特殊的地址，用NULL赋值的指针指向的地址为0而不是随机的地址。只有当你准备使用这个地址时有效。不要对NULL地址取值，否则会产生段错误。

- 指针和数组
    - C语言的数组表示一段连续的内存空间，用来存储多个特定类型的对象。与之相反，指针用来存储单个内存地址。数组和指针不是同一种结构因此不可以互相转换。而数组变量指向了数组的第一个元素的内存地址。
    - 一个数组变量是一个常量。即使指针变量指向同样的地址或者一个不同的数组，也不能把指针赋值给数组变量。也不可以将一个数组变量赋值给另一个数组。然而，可以把一个数组变量赋值给指针，这一点似乎让人感到费解。把数组变量赋值给指针时，实际上是把指向数组第一个元素的地址赋给指针。

```
int myarray[4] = {1,2,3,0};
int *ptr = myarray;
printf("*ptr=%d\n", *ptr);
 
// 数组变量是常量，不能做下面的赋值
// myarray = ptr
// myarray = myarray2
// myarray = &myarray2[0]
```
第1行初始化了一个int数组，第2行用数组变量初始化了一个int指针。由于数组变量实际上是第一个元素的地址，因此我们可以把这个地址赋值给指针。这个赋值与int *ptr = &myarray[0]效果相同，显示地把数组的第一个元素地址赋值到了ptr引用。这里需要注意的是，这里指针需要和数组的元素类型保持一致，除非指针类型为void。

- 指针与`结构体`
就像数组一样，指向结构体的指针存储了结构体第一个元素的内存地址。与数组指针一样，结构体的指针必须声明和结构体类型保持一致，或者声明为void类型。

```
struct person {
  int age;
  char *name;
};
struct person first;
struct person *ptr;
 
first.age = 21;
char *fullname = "full name";
first.name = fullname;
ptr = &first;
 
printf("age=%d, name=%s\n", first.age, ptr->name);
```

第1至6行声明了一个person结构体，一个变量指向了一个person结构体和指向person结构体的指针。第8行为age成员赋了一个int值。第9至10行我们声明了一个char指针并赋值给一个char数组并赋值给结构体name成员。第11行我们把一个person结构体引用赋值给结构体变量。

第13行我们打印了结构体实例的age和name。这里需要注意两个不同的符号，’.’ 和 ‘->’ 。结构体实例可以通过使用 ‘.’ 符号访问age变量。对于结构体实例的指针，我们可以通过 ‘->’ 符号访问name变量。也可以同样通过(*ptr).name来访问name变量。

# 结构体
## 概述
### 什么事结构体
1. C语言中的数组，用法跟其他语言差不多。当一个整体由多个数据构成时，我们可以用数组来表示这个整体，但是数组有个特点：内部的每一个元素都必须是相同类型的数据。
2. 在实际应用中，我们通常需要由不同类型的数据来构成一个整体，比如学生这个整体可以由姓名、年龄、身高等数据构成，这些数据都具有不同的类型，姓名可以是字符串类型，年龄可以是整型，身高可以是浮点型。
3. 为此，C语言专门提供了一种构造类型来解决上述问题，这就是结构体，它允许内部的元素是不同类型的。

### 结构体的定义
1. 定义形式：结构体内部的元素，也就是组成成分，我们一般称为"成员"。
结构体的一般定义形式为：
```
struct　结构体名{     
     类型名1　成员名1;     
     类型名2　成员名2;     
     ……     
     类型名n　成员名n;     
 };
```
2. 先定义结构体类型，再定义变量。
```
struct Student {
     char *name;
     int age;
 }; 
 struct Student stu;
```
3. 定义和变量同时进行
```
struct Student {
    char *name;
    int age;
} stu;
// 结构体变量名为stu
```
4. 直接定义结构体类型变量，省略类型名
```
struct {
    char *name;
    int age;
} stu;
// 结构体变量名为stu
```

### 注意事项
- 不可以在结构体本身进行递归定义
- 可以包含别的结构体

### 内存分配
- 定义结构体类型，只是说明了该类型的组成情况，并没有给它分配存储空间，就像系统不为int类型本身分配空间一样。只有当定义属于结构体类型的变量时，系统才会分配存储空间给该变量。
```
struct Student {
     char *name;
     int age;
 };
struct Student stu;
// 第1~4行并没有分配存储空间，当执行到第6行时，系统才会分配存储空间给stu变量。
 ```
- 结构体变量占用的内存空间是其成员所占内存之和，而且各成员在内存中按定义的顺序依次排列。
```
struct Student {
     char *name; // 姓名
     int age; // 年龄
     float height; // 身高
 };
// 在16位编译器环境下，一个Student变量共占用内存：2 + 2 + 4 = 8字节。
```

### 结构体初始化
- 将各成员的初值，按顺序地放在一对大括号{}中，并用逗号分隔，一一对应赋值。
比如初始化Student结构体变量stu
```
 struct Student {
     char *name;
     int age;
 }; 
struct Student stu = {“NJ", 27};
```
- 只能在定义变量的同时进行初始化赋值，初始化赋值和变量的定义不能分开，下面的做法是错误的
```
struct Student stu;
stu = {“NJ", 27};
```

### 操作结构体
1. 一般对结构体变量的操作是以成员为单位进行的，引用的一般形式为：结构体变量名.成员名
```
struct Student {
     char *name;
     int age;
 };
 struct Student stu;
 // 访问stu的age成员
 stu.age = 27;
// 第9行对结构体的age成员进行了赋值。"."称为成员运算符，它在所有运算符中优先级最高
```

2. 如果某个成员也是结构体变量，可以连续使用成员运算符"."访问最低一级成员
```
struct Date {
       int year;
       int month;
       int day;
  };
  
  struct Student {
      char *name;
      struct Date birthday;
 };
 
 struct Student stu;
 stu.birthday.year = 1986;
 stu.birthday.month = 9;
 stu.birthday.day = 10;
```

3. 相同类型的结构体变量之间可以进行整体赋值
```
struct Student {
      char *name;
      int age;
};  
struct Student stu1 = {“NJ”, 27};  
// 将stu1直接赋值给stu2
struct Student stu2 = stu1; 
printf("age is %d", stu2.age);
```

4. 将结构体变量作为函数参数进行传递时，其实传递的是全部成员的值，也就是将实参中成员的值一一赋值给对应的形参成员。因此，形参的改变不会影响到实参。

5. 指向结构体的指针
    每个结构体变量都有自己的存储空间和地址，因此指针也可以指向结构体变量
    - 结构体指针变量的定义形式：struct 结构体名称 *指针变量名
    - 有了指向结构体的指针，那么就有3种访问结构体成员的方式
    - 结构体变量名.成员名
    - (*指针变量名).成员名
    - 指针变量名->成员名

# 枚举
## 基本概念
>枚举是C语言中的一种基本数据类型，并不是构造类型，它可以用于声明一组常数。当一个变量有几个固定的可能取值时，可以将这个变量定义为枚举类型。比如，你可以用一个枚举类型的变量来表示季节，因为季节只有4种可能的取值：春天、夏天、秋天、冬天。

### 定义
1. 一般形式为：enum　枚举名　{枚举元素1,枚举元素2,……};
```
enum Season {
	spring, 
	summer, 
	autumn, 
	Winter
}; 
```
2. 先定义枚举类型，再定义枚举变量
```
enum Season {
	spring, 
	summer, 
	autumn, 
	Winter
}; 
2.enum Season s;
```
3. 定义枚举类型的同时定义枚举变量
```
enum Season {
	spring, 
	summer,
	autumn,
 	winter
} s;
```
4. 省略枚举名称，直接定义枚举变量
```
enum{
  spring,
     summer,
     autumn, 
     winter
} s;
```

### 枚举使用的注意
1. C语言编译器会将枚举元素(spring、summer等)作为整型常量处理，称为枚举常量。
2. 枚举元素的值取决于定义时各枚举元素排列的先后顺序。默认情况下，第一个枚举元素的值为0，第二个为1，依次顺序加1。
```
enum Season {spring, summer, autumn, winter};
// 也就是说spring的值为0，summer的值为1，autumn的值为2，winter的值为3
```
3. 也可以在定义枚举类型时改变枚举元素的值
```
enum season {spring, summer=3, autumn, winter};
// 没有指定值的枚举元素，其值为前一元素加1。也就说spring的值为0，summer的值为3，autumn的值为4，winter的值为5
```

### 赋值
- 可以给枚举变量赋枚举常量或者整型值
```
enum Season {spring, summer, autumn, winter} s;
s = spring; // 等价于 s = 0;
s = 3; // 等价于 s = winter;
```

### 遍历枚举元素
```
enum Season {spring, summer, autumn, winter} s;
// 遍历枚举元素
for (s = spring; s <= winter; s++) {
    printf("枚举元素：%d \n", s);
}
```
