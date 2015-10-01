---
layout: post
title: 数组中出现次数超过一半的数字
date: 2015-08-26
categories: Algorithm
tags: algorithm array
---

## 1. 问题描述

数组中有一个数字出现的次数超过了数组长度的一半，请找出这个数字。

## 2. 解题思路

思路一，借鉴快速排序的思路：

- 在数组中随机选择一个数字；
- 调整数组数字的顺序，使得比选中的数字小的数字都在它的左边，比它大的都在右边。
- 如果选中的数字的下标刚好是n/2，那么这个数字就是数组的中位数。否则递归查找；

思路二：

- 这个数字出现的次数比其他所有数字出现的次数的和还要多；因此设定两个值，一个是数字，一个是出现的次数；
- 如果下一个数字和当前数字相同，++；
- 如果下一个数字和当前数字不同，--；
- 如果次数等于0，保留下一个数字，并置次数为1；

## 3. 参考代码

**解法一**

{% highlight c++ %}

bool g_bInputInvalid = false;

int Swap(int* a, int* b) {
	int tmp = *a;
	*a = *b;
	*b = tmp;
}

bool CheckInvalidArray(int* numbers, int length);
bool CheckMoreThanHalf(int* numbers, int length, int number);

//快排
int Partition(int data[], int length; int start, int end) {
	int nTemp = data[end];
	int i = nLow, j = nLow-1;
	for(; i < nHigh; i++) {
		if(data[i] < nTemp) {
			j++;
			if(i != j) 
				Swap(data[i], data[j]);
		}
	}
	Swap(data[j+1], data[end]);
}

int MoreThanHalfNum(int* numbers, int length) {
	if(CheckInvalidArray(numbers, length))	
		return 0;

	int middle = length >> 1;
	int start = 0;
	int end = length - 1;
	int index = Partition(numbers, length, start, end);

	while(index != middle) {
		if(index > middle) {
			end = index-1;
			index = Partition(numbers, length, start, end);
		} else {
			start = index+1;
			index = Partition(numbers, length, start, end);
		}
	}

	int result = numbers[middle];
	if(!CheckMoreThanHalf(numbers, length, result))
		result = 0;
	
	return result;
}

//检查是否为无效输入
bool CheckInvalidArray(int* numbers, int length) {
	g_bInputInvalid = false;

	if(numbers == NULL || length <= 0)
		g_bInputInvalid = true;

	return g_bInputInvalid;
}

//检查有查找的数字是否出现次数超过一半
bool CheckMoreThanHalf(int* numbers, int length, int number) {
	int times = 0;
	for(int i = 0; i < length; i++) {
		if(numbers[i] == number)
			times++;
	}

	bool isMoreThanHalf = true;
	if(times * 2 < length) {
		g_bInputInvalid = true;
		isMoreThanHalf = false;
	}
	return isMoreThanHalf;
}
{% endhighlight c++ %}

**解法二**
{% highlight c++ %}
int MoreThanHalfNum(int* numbers, int length) {
	if(CheckInvalidArray(numbers, length)) {
		return 0;
	}

	int result = numbers[0];
	int times = 1;
	for(int i = 1; i < length; i++) {
		if(times == 0) {
			result = numbers[i];
			times = 1;
		} else if(numbers[i] == result)
			times++;
		else
			times--;
	}

	if(!CheckMoreThanHalf(numbers, length, result))
		result = 0;

	return result;
}
{% endhighlight c++ %}

## 4. 思考

快排的代码需要熟记于心，理解如何swap；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)