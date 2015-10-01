---
layout: post
title: 数组中的逆序对
date: 2015-08-31
categories: Algorithm
tags: algorithm
---

## 1. 问题描述

在数组中的两个数字如果前面一个数字大于后面的数字，则着两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数；如在数组{7,5,6,4}中，一共有五个逆序对；

## 2. 解题思路

思路一：

- 把每个数字分别和后面的每一个数字对比；
- 时间复杂度为O(n^2)

思路二：

- 把数组分成两个子数组；
- 先统计出子数组内部的逆序对的数目；
- 再统计出两个相邻子数组之间的逆序对，这个过程相当于归并排序；详见剑指offer。

## 3. 参考代码

{% highlight c++ %}
int InversePairsCore(int* data, int* copy, int start, int end);
int InversePairs(int* data, int length) {
	if(data == NULL || length == 0) 
		return 0;

	int* copy = new int[length];
	for(int i = 0; i < length; i++) 
		copy[i] = data[i];

	int count = InversePairsCore(data, copy, 0, length-1);
	delete[] copy;

	return count;
}

int InversePairsCore(int* data, int* copy, int start, int end) {
	if(start == end) {
		copy[start] = data[end];
		return 0;
	}

	int length = (end - start) / 2;

	//递归求左边数组里面的逆序对；
	int left = InversePairsCore(copy, data, start, start+length);
	//递归求左边数组里面的逆序对；
	int right = InversePairsCore(copy, data, start+length+1, end);

	//i初始化为前半段最后一个数字的下标；
	int i = start + length;
	//j初始化为后半段最后一个数字的下标；
	int j = end;
	int indexCopy = end;
	int count = 0;
	//求两个相邻数组之间的逆序对；
	while(i >= start && j >= start+length+1) {
		if(data[i] > data[j]) {
			copy[indexCopy--] = data[i--];
			count += (j - start - length);
		} else {
			copy[indexCopy--] = data[j--];
		}
	}
	
	//复制排序；
	for( ; i >= start; )
		copy[indexCopy--] = data[i--];

	for( ; j >= start+length+1; )
		copy[indexCopy--] = data[j--];

	return left + right + count;
}
{% endhighlight c++ %}

## 4. 思考

- 递归！递归！！递归！！！
- 归并排序；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)