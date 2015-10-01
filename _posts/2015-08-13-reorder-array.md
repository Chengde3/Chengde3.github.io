---
layout: post
title: 调整数组顺序使奇数位于偶数前面
date: 2015-08-13
categories: Algorithm
tags: algorithm
---

## 1. 问题描述

输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数位于数组的前半部分，所有的偶数位于数组的后半部分；

## 2. 解题思路

设置两个指针，一个指向开始，一个指向结尾，移动指针病交换即可；

## 3. 参考程序

{% highlight c++ %}
//一般解法
void ReorderOddEven(int* pData, unsigned int length) {
	//空指针判断
	if(pData == NULL || length == 0)
		return;

	int* pBegin = pData;
	int* pEnd = pData + length - 1;

	while(pEnd < pBegin) {
		//向后移动pBegin，直到它指向偶数
		while(pBegin < pEnd && (*pBegin & 0x1) != 0)
			pBegin++;

		//向前移动pEnd，直到它指向奇数
		while(pBegin < pEnd && (*pEnd & 0x1) == 0) 
			pEnd--;

		if(pBegin < pEnd) {
			int temp = *pBegin;
			*pBegin = *pEnd;
			*pEnd = temp;
		}
	}
}


//通用解法
void Reorder(int* pData, unsigned int length, bool (*func)(int)) {
	if(pData == NULL || length == 0)
		return 0;

	int* pBegin = pData;
	int* pEnd = pData + length - 1;

	while(pBegin < pEnd) {
		while(pBegin < pEnd && !func(*pBegin))
			pBegin++;
		while(pBegin < pEnd && func(*pEnd)) 
			pEnd--;

		if(pBegin < pEnd) {
			int temp = *pBegin;
			*pBegin = *pEnd;
			*pEnd = temp;
		}
	}
}

bool isEven(int n) 
	return (n & 1) == 0;

void ReorderOddEven(int* pData, unsigned int length) {
	Reorder(pData, length, isEven);	
}
{% endhighlight c++%}

## 4. 思考

一般的解法并不难，关键在于指针的操作。其次考虑扩展性，估计现在自己还很难做到。

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)