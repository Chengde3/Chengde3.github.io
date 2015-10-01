---
layout: post
title: 行列递增矩阵的查找(杨氏矩阵)
date: 2015-08-07
categories: Algorithm
tags: algorithm 剑指offer
---

## 1. 问题定义

在一个m行n列二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

例子可以参考[这个链接](http://taop.marchtea.com/04.02.html)

## 2. 解题思路

首先选取数组中右上角的数字，会有如下三种情况：

- 数字等于要查找的数字，则查找过程结束；
- 数字大于要查找的数字，剔除这个数字所在的列；
- 数字小于要查找的数字，剔除这个数字所在的行；

## 3. 参考代码

{% highlight c %}

bool Find(int* matrix, int rows, int columns, int number) {
	bool found = false;

	if(matrix != NULL && rows > 0 && columns > 0) {
		int row = 0;
		int column = columns - 1;
		while(row < rows && column >= 0) {
			if(matrix[row * columns + column] == number) {
				found = true;
				break;
			else if(matrix[row * columns + column] > number)
				column--;
			else
				row++;
		}
	}
	return found;
}

int main() {
	//注：下面写的不正确，因为jekyll会报错。
	int matrix[][4] = {1,2,8,9}, {2,4,9,12}, {4,7,10,13}, {6,8,11,15};
	bool result = Find((int*)matrix, 4, 4, 7);
	printf("%d\n", result);
	return 0;
}
 	
{% endhighlight c %}

## 4. 注意事项

- 要注意判断矩阵为空的情况；

## 5. 参考文献

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)
- [行列递增矩阵的查找](http://taop.marchtea.com/04.02.html)