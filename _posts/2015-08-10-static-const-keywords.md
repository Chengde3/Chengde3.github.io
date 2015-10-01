---
layout: post
title: C++中的static和const
date: 2015-08-10
categories: C++
tags: c++ const static
---

## 1. static关键字的用法

### 1.1 扩展生存周期

针对普通局部变量和static局部变量来说的；static局部变量的生存期不再时当前作用域，而是整个程序的生存期；

### 1.2 限制作用域

相对于普通全局变量和static全局变量来说的；对于全局变量而言，不论时普通全局变量还是static全局变量，期存储区域都是静态存储区。区别在于以下几个方面：

- 普通的全局变量和函数，其作用域时整个程序或者项目，外部文件可以通过extern关键字访问该变量和函数。
- static全局变量和函数，其作用域是当前cpp文件，其他的cpp文件不能访问该变量和函数。

### 1.3 数据的唯一性

这是C++对关键字的重用。主要指静态数据成员/成员函数；申明该成员时属于一个类而不是属于此类的任何特定对象的变量和函数；

## 2. const关键字

### 2.1 基本概念

使用const修饰的类型是常类型。常类型的变量或对象的值不能被改变。

### 2.2 const指针和指向const的指针

{% highlight c++ %}
//const指针
int* const a = &[1];
//指向const的指针
const int* p = &[1];
{% endhighlight c++ %}

- 如果const位于星号的左侧，const用来修饰指针指向的变量，即指针指向为常量；
- 如果const位于星号的右侧，const就是修饰指针本身，即指针本身是常量；


## 3. 参考文献

- [[C/C++]static关键字用法总结[转载]](http://www.cnblogs.com/chengxin1985/archive/2009/02/06/1384997.html)
- [【C++ const的各种用法详解】【const用法深入浅出】](http://www.cnblogs.com/wintergrass/archive/2011/04/15/2015020.html)
- [C++中const关键字的使用方法，烦透了一遍一遍的搜，总结一下，加深印象！！！](http://www.cnblogs.com/jiabei521/p/3335676.html)
- [const 指针与指向const的指针](http://www.cnblogs.com/younes/archive/2009/12/02/1615348.html)(例子不错)