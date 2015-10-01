---
layout: post
title: 斐波那契数列
date: 2015-08-09
categories: Algorithm
tags: algorithm fabonacci
---

## 1. 问题描述

输入n，求斐波那契数列的第n项。

## 2. 解题思路

思路一：

- 递归法：使用斐波那契数列的公式递归求解；

思路二：

- 循环法：根据f0,f1求f2,根据f1,f2求f3......

## 3. 参考代码

{% highlight c++ %}
//递归法
long long Fibonacci(unsigned int n) {
	if(n <= 0) 
		return 0;
	if(n == 1) 
		return 1;

	return Fibonacci(n-1) + Fibonacci(n-2);
}


//循环法
long long Fibonacci(unsigned int n) {
	int result[2] = {0, 1};
	if(n < 2) 
		return result[n];

	long long fibNMinusOne = 1;
	long long fibNMinusTwo = 0;
	long long fibN = 0;
	for(unsigned int i = 2; i <= n; i++) {
		fibN = fibNMinusOne + fibNMinusTwo;
		fibNMinusTwo = fibNMinusOne;
		fibNMinusOne = fibN;
	}
	return fibN;
}
{% endhighlight c++ %}

## 4. 注意事项

- 上述的递归代码效率太低，原因在于重复计算太多。改进的方向是**把已经计算的中间项保存起来，避免重复计算**
- 基于递归实现的代码比基于循环实现的代码要简洁，且更加容易实现。面试时应该优先使用递归的方法编程。
- 递归是函数调用自身，因此会有时间和空间的消耗；
- 递归调用的层次太多可能会造成调用栈溢出。

## 5. 问题扩展

### 5.1 扩展一

#### 5.1.1 问题定义

一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级台阶总共有多少种跳法；

#### 5.1.2 解题思路

- 用数学归纳法归纳出规律，就是斐波那契数列的求解；

### 5.2 扩展二

#### 5.2.1 问题定义

有一个2X1的小矩形（两个1X1的方块），用这种矩形去无重叠地覆盖一个2X8的大矩形，总共有多少种方法；

#### 5.2.2 解题思路

- 用数学归纳法归纳出规律，还是斐波那契数列的求解。。。。。。

## 6. 参考文献

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)