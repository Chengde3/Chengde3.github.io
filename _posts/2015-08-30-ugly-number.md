---
layout: post
title: 丑数
date: 2015-08-30
categories: Algorithm
tags: algorithm
---

## 1. 问题描述

我们把只包含因子2,3和5的数称为丑数。求按从小到大的顺序的第1500个丑数。习惯上把1当做第一个丑数；

## 2. 解题思路

思路一：

- 逐个判断每个数字是否是丑数。即把每一个数字连续除以2,再连续除以3,最后连续除以5。如果最后结果为1，则这个数就是丑数。

思路二：

- 创建数组保存已经找到的丑数；
- 创建一个排序数组，计其中的最大的数为M，然后将里面的数字乘以2，乘以3，乘以5，找到结果中第一个比M大的数，记为M2，M3，M5。那么下一个丑数就是这三个数中的最小值；

## 3. 参考代码

//思路一参考代码
{% highlight c++ %}
bool IsUgly(int number) {
	while(number % 2 == 0)
		number /= 2;
	while(number % 3 == 0)
		number /= 3;
	while(number % 5 == 0)
		number /= 5;

	return (number == 1) ? true : false;
}

int GetUglyNumber(int index) {
	if(index <= 0)
		return 0;

	int number = 0;
	int uglyFound = 0;
	while(uglyFound < index) {
		number++;
		if(IsUgly(number))
			++uglyFound;
	}

	return number;
}
{% endhighlight c++ %}

//思路二参考代码；
{% highlight c++ %}
int Min(int number1, int number2, int number3);
int GetUglyNumber_Solution2(int index) {
	if(index < 0)
		return 0;

	int *pUglyNumbers = new int[index];
	pUglyNumbers[0] = 1;
	int nextUglyIndex = 1;

	int *pMultiply2 = pUglyNumbers;
	int *pMultiply3 = pUglyNumbers;
	int *pMultiply5 = pUglyNumbers;

	while(nextUglyIndex < index) {
		int min = Min(*pMultiply2 * 2, *pMultiply3 * 3 , *pMultiply5 * 5);
		pUglyNumbers[nextUglyIndex] = min;

		while(*pMultiply2 * 2 <= pUglyNumbers[nextUglyIndex])
			pMultiply2++;
		while(*pMultiply3 * 3 <= pUglyNumbers[nextUglyIndex])
			pMultiply3++;
		while(*pMultiply5 * 5 <= pUglyNumbers[nextUglyIndex])
			pMultiply5++;

		nextUglyIndex++;
	}

	int ugly = pUglyNumbers[nextUglyIndex-1];
	delete[] pUglyNumbers;
	return ugly;
}

int Min(int number1, int number2, int number3) {
	int min = (number1 < number2) ? number1 : number2;
	min = (min < number3) ? min : number3;
	return min;
}
{% endhighlight c++ %}

## 4. 思考

- 善于用技巧，思考数据的本质以及规律，而不是一味用蛮力；
- 此题还有一个相关的题目，就是质因数分解；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)