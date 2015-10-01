---
layout: post
title: 数组中只出现一次的数字
date: 2015-08-31
categories: Algorithm
tags: algorithm
---

## 1. 问题描述

一个整型数组里除了两个数字之外，其他的数字都出现了两次。写程序找出着两个只出现一次的数字。要求时间复杂度为O(n)，空间复杂度为O(1)；

## 2. 解题思路

对于只有一个数字出现一次，其余出现两次的好办，只需异或即可；考虑将数组分成两个子数组，使得每个子数组包含一个只出现一次的数字，二其他数字都出现两次；

思路如下：

- 依次异或数组中的每个数字；
- 在结果数字中找到第一个为1的位的位置，记为第n位；
- 以第n位是否为1为标准把原数组分为两个子数组；
- 在两个子数组中对每个元素做异或即可；

## 3. 参考代码

{% highlight c++ %}
unsigned int FindFirstBitIs1(int num);
bool IsBit1(int num, unsigned int indexBit);
void FindNumbsAppearOnce(int data[], int length, int* num1, int* num2) {
	if(data == NULL || length < 2)
		return;

	int resultExclusiveOR = 0;
	for(int i = 0; i < length; i++) 
		resultExclusiveOR ^= data[i];

	unsigned int indexOf1 = FindFirstBitIs1(resultExclusiveOR);

	*num1 = *num2 = 0;
	for(int j = 0; j < length; j++) {
		if(IsBit1(data[j], indexOf1))
			*num1 ^= data[j];
		else 
			*num2 ^= data[j];
	}
}

unsigned int FindFirstBitIs1(int num) {
	int indexBit = 0;
	while((num & 1) == 0 && (indexBit < 8 * sizeof(int))) {
		num = num >> 1;
		indexBit++;
	}
	return indexBit;
}

bool IsBit1(int num, unsigned int indexBit) {
	num = num >> indexBit;
	return (num & 1);
}
{% endhighlight c++ %}

## 4. 思考

- 移位运算；
- 逻辑运算；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)