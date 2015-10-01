---
layout: post
title: 连续子数组的最大和
date: 2015-08-29
categories: Algorithm
tags: algorithm array
---

## 1. 问题描述

输入一个整型数组，数组里面有正数也有负数。数组中一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。要求时间复杂度为O(n);

## 2. 解题思路

举例子发现规律如下：

- 如果之前累计的值小于0，那么累计值变为当前数字的值；
- 如果之前累计的值大于0，那么累计值加上当前数字的值；
- 如果累计的值大于之前的最大值，那么更新最大值；

## 3. 参考代码

{% highlight c++ %}
bool g_InvalidInput = false;

int FindGreatestSumOfSubArray(int* pData, int nLength) {
	if((pData == NULL) || nLength < 0) {
		g_InvalidInput = false;
		return 0;
	}

	g_InvalidInput = false;

	int nCurSum = 0;
	int nGreatestSum = 0x80000000;
	for(int i = 0; i < nLength; i++) {
		if(nCurSum < 0) 
			nCurSum = pData[i];
		else 
			nCurSum += pData[i];

		if(nCurSum > nGreatestSum) 
			nGreatestSum = nCurSum;
	}

	return nGreatestSum;
}
{% endhighlight c++ %}

## 4. 思考

- 遇到复杂问题，可以通过具体的例子来分析其中的规律；
- 动态规划还未掌握；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)