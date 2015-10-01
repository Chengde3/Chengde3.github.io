---
layout: post
title: 数组中重复的数字
date: 2015-09-01
categories: Algorithm
tags: algorithm
---

## 1. 问题描述

在一个长度为n的数组里的所有数字都在0～n-1的范围内。数组中的某些数字时重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。例如，如果输入长度为7的数组{2,3,1,0,2,5,3}，那么对应的输出是重复的数字2或者3；

## 2. 解题思路

思路一：

- 排序后查找；

思路二：

- 使用hashmap；

思路三：

- 扫描数组，当扫描到下标为i的数字时，比较这个数字m是不是等于从；
- 如果等于，接着扫描；
- 如果不等于，拿它和第m个数字进行比较；
- 如果和第m个数字相等，则是重复的数字；
- 如果和第m个数字不相等，则进行交换，把m放在该放的位置；

## 3. 参考代码

//思路三参考代码
{% highlight c++ %}
bool duplicate(int numbers[], int length, int* duplication) {
	if(numbers == NULL || length <= 0)
		return false;

	for(int i = 0; i < length; i++) 
		if(numbers[i] < 0 || numbers[i] > length - 1)
			return false;

	for(int i = 0; i < length; i++) {
		while(numbers[i] != i) {
			if(numbers[i] == numbers[numbers[i]]) {
				*duplication = numbers[i];
				return true;
			}

			//swap numbers[i] and numbers[numbers[i]];
			int tmp = numbers[i];
			numbers[i] = numbers[tmp];
			numbers[tmp] = tmp;
		}
	}

	return false;
}
{% endhighlight c++ %}

## 4. 思考

无；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)