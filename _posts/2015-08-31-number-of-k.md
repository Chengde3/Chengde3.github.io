---
layout: post
title: 数字在排序数组中出现的次数
date: 2015-08-31
categories: Algorithm
tags: algorithm
---

## 1. 问题描述

统计一个数字在排序数组中出现的次数。

## 2. 解题思路

- 一般的解题思路时间复杂度为O(n)
- 可以参考二分查找的方法，找出第一个出现的数字和最后出现的数字即可；

## 3. 参考代码

{% highlight c++ %}

int GetFirstK(int* data, int length, int k, int start, int end) {
	if(start > end)
		return -1;

	int middleIndex = (start + end) / 2;
	int middleData = data[middleIndex];

	if(middleData == k) {
		//注意这里的判断条件，判断[data[middleIndex-1] != k时需要保证middleIndex > 0;
		if((middleIndex > 0 && data[middleIndex-1] != k) || middleIndex == 0)
			return middleIndex;
		else 
			end = middleIndex - 1;
	} else if(middleIndex > k)
		end = middleIndex - 1;
	else 
		start = middleIndex + 1;

	return GetFirstK(data, length, k, start, end);
}

int GetLastK(int* data, int length, int k, int start, int end) {
	if(start > end)
		return -1;

	int middleIndex = (start + end) / 2;
	int middleData = data[middleIndex];

	if(middleData == k) {
		if((middleIndex < length-1 && data[middleIndex+1] != k) || middleIndex == length - 1)
			return middleIndex;
		else 
			start = middleIndex + 1;
	} else if(middleIndex < k)
		start = middleIndex + 1;
	else 
		end = middleIndex - 1;

	return GetLastK(data, length, k, start, end);
}

int GetNumberOfK(int* data, int length, int k) {
	int number = 0;
	if(data != NULL && length > 0) {
		int first = GetFirstK(data, length, k, 0, length-1);
		int last = GetLastK(data, length, k, 0, length-1);

		if(first > -1 && last > -1)
			number = last - first + 1;
	}
	return number;
}
{% endhighlight c++ %}

## 4. 思考

无；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)