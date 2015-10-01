---
layout: post
title: 顺时针打印矩阵
date: 2015-08-14
categories: Algorithm
tags: algorithm matrix
---

## 1. 问题描述

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

## 2. 解题思路

按圈打印。需要注意的是一些边界条件。关键在于写代码之前理清思路。

## 3. 参考代码

{% highlight c++ %}
void PrintMatrixClockwisely(int** numbers, int columns, int rows) {
	//异常输入
	if(numbers == NULL || columns <= 0 || rows <= 0) 
		return;

	//以左上角的坐标作为标识
	int start = 0;
	while(columns > start * 2 && rows > start * 2) {
		PrintMatrixInCircle(numbers, columns, rows, start);
		++start;
	}
}

void PrintMatrixInCircle(int** numbers, int columns, int rows, int start) {
	int endX = columns - 1 - start;
	int endY = rows - 1 - start;

	//从左向右打印一行
	for(int i = start; i <= endX; i++) {
		int number = numbers[start][i];
		printNumber(number);
	}

	//从上到下打印一列
	if(start < endY) {
		for(int i = start + 1; i <= endY; i++){
			int number = numbers[i][endX];
			printNumber(number);
		}
	}

	//从右向左打印一行
	if(start < endX && start < endY) {
		for(int i = endX - 1; i >= start; i--) {
			int number = numbers[endY][i];
			printNumber(number);
		}
	}

	//从下到上打印一列
	if(start < endX && start < endY - 1) {
		for(int i = endY - 1; i >= start + 1; i--) {
			int number = numbers[i][start];
			printNumber(number);
		}
	}
}
{% endhighlight c++ %}

## 4. 思考

边界处理很重要，想清楚了再写代码；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)