---
layout: post
title: 圆圈中最后剩下的数字
date: 2015-09-01
categories: Algorithm
tags: algorithm
---

## 1. 问题描述

0,1,2,...,n-1这n个数字排成一个圆圈，从数字0开始每次从这个圆圈中删除第m个数字。求出这个圆圈里剩下的最后一个数字；

## 2. 解题思路

思路一：

- 用环形链表来模拟圆圈，每次当迭代器扫描到链表末尾的时候，把迭代器移到链表的头部；

思路二：

- 分析删除数字得到规律；（详见剑指offer）

## 3. 参考代码

//思路一参考代码
{% highlight c++ %}
int LastRemaining(unsigned int n, unsigned int m) {
	if(n < 1 || m < 1)
		return -1;

	unsigned int i = 0;

	list<int> numbers;
	for(i = 0; i < n; i++)
		numbers.push_back(i);

	list<int>::iterator current = numbers.begin();
	while(numbers.size() > 1) {
		for(int i = 1; i < m; i++) {
			current++;
			if(current == numbers.end())
				current = numbers.begin();
		}

		list<int>::iterator next = current + 1;
		if(next == numbers.end())
			next = numbers.begin();

		numbers.erase(current);
		current = next;
	}

	return *current;
}
{% endhighlight c++ %}

//思路二参考代码
{% highlight c++ %}
int LastRemaining(unsigned int n, unsigned int m) {
	if(n < 1 || m > 1)
		return -1;

	int last = 0;
	for(int i = 2; i <= n; i++) 
		last = (last + m) % i;

	return last;
}
{% endhighlight c++ %}

## 4. 思考

无；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)