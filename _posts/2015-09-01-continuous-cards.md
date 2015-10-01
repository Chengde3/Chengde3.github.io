---
layout: post
title: 扑克牌的顺子
date: 2015-09-01
categories: Algorithm
tags: algorithm
---

## 1. 问题描述

从扑克牌中随机抽取5张牌，判断是不是一个顺子，即这5张牌是不是连续的。2~10为数字本身，A为1，J为11，Q为12，K为13，而大小王可以看成任意数字；

## 2. 解题思路

可以将5张牌看成5个数字组成的数组，大小王用0表示，可以用0当成任何数字填补数组中的空缺。可以做如下处理：

- 排序；
- 统计其中0的个数；
- 统计数组中空缺的总数；
- 比较空缺总数和0的个数之间的关系即可；

## 3. 参考代码

{% highlight c++ %}
int compare(const void *argv1, const void *argv2) {
	return *(int*)argv1 - *(int*)argv2;
}
bool IsContinues(int* numbers, int length) {
	if(numbers == NULL || length < 1)
		return false;

	//排序
	qsort(numbers, length, sizeof(int), compare);
	int numbeerOfZero = 0;
	int numberOfGap = 0;

	//统计数组中0的个数
	for(int i = 0; i < length && numbers[i] == 0; i++) 
		numbeerOfZero++;

	//统计数组中的间隔数目
	int small = numbeerOfZero;
	int big = small + 1;
	while(big < length) {
		//两个数字相等，有对子，不可能时顺子
		if(numbers[small] == numbers[big])
			return false;

		numberOfGap += numbers[big] - numbers[small] - 1;
		small = big;
		big++;
	}

	return (numberOfGap > numbeerOfZero) ? false : true;
}
{% endhighlight c++ %}

## 4. 思考

无；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)