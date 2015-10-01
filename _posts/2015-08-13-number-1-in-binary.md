---
layout: post
title: 二进制中1的个数
date: 2015-08-13
categories: Algorithm
tags: algorithm binary
---

## 1. 问题描述

实现一个函数，输入一个整数，输出该二进制表示中1的个数。

## 2. 解题思路

有如下三种思路：

- 把整数与1做与运算，同时右移整数；但是如果输入负数会造成死循环；
- 把整数与1做与运算，同时左移1；需要比较32次；
- **把一个整数减去1，再和原整数做与运算，会把该整数的最右边的一个1变成0。所以一个整数的二进制中有多少1，就会进行多少次操作；（可以画图演算）**

## 3. 参考代码

{% highlight c++ %}
//可能会引起死循环
int NumberOf1(int n) {

	int num = 0;
	while(n) {
		if(n & 1)
			num ++;

		n = n >> 1;
	}
	return num;
}

//32次比较
int NumberOf12(int n) {
	int num = 0;
	unsigned int flag = 1;
	while(flag) {
		if(n & flag) 
			num++;

		flag = flag << 1;
	}
	return num;
}

//1的个数有多少个，则比较多少次
int NumberOf13(int n) {
	int num = 0;

	while(n) {
		++ num;
		n = (n - 1) & n;
	}
	return	num;
}
{% endhighlight c++ %}

## 4. 注意事项

- 需要考虑特殊输入；
- 一个思路：整数减1后再和整数做与运算，会把整数的二进制表示中的最右边一个1变成0；


## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)