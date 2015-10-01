---
layout: post
title: 和为s的连续正数序列
date: 2015-08-31
categories: Algorithm
tags: algorithm
---

## 1. 问题描述

输入一个正数s，打印出所有和为s的连续正数序列（至少包含两个数）。例如输入15，由于1+2+3+4+5=4+5+6=7+8=15，所有结果打印出连续3个连续序列1~5,4~6,7~8；

## 2. 解题思路

- 设置两个变量，small和big，初始化分别为1,2，计算sum；
- 如果sum < s，big++;
- 如果sum > s, small++;

## 3. 参考代码

{% highlight c++ %}
void PrintContinuousSequence(int small, int big);
void FindContinuousSequence(int sum) {
	if(sum < 3) 
		return;

	int small = 1;
	int big = 2;
	int middle = (1 + sum ) / 2;
	int curSum = small + big;

	while(small < middle) {
		if(curSum == sum)
			PrintContinuousSequence(small, big);

		while(curSum > sum && small < middle) {
			curSum -= small;
			small++;
			if(curSum == sum)
				PrintContinuousSequence(small, big);
		}

		big++;
		curSum += big;
	}
}

void PrintContinuousSequence(int small, int big) {
	for(int i = small; i <= big; i++) 
		printf("%d ", i);

	printf("\n");
}
{% endhighlight c++ %}

## 4. 思考

无；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)