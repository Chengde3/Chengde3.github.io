---
layout: post
title: 构建乘积数组
date: 2015-09-02
categories: Algorithm
tags: algorithm
---

## 1. 问题描述

给定一个数组A[0,1,...,n-1]，请构建一个数组B[0,1,...,n-1],其中B中的元素B[i]=A[0]xA[1]xA[2]x...xA[i-1]xA[i+1]x...xA[n-1]，不能使用除法；

## 2. 解题思路

思路一：

- 如果可以使用除法，需要特别注意元素等于0的情况；

思路二：

- 连乘n-1个数字得到B[i]。时间复杂度为O(n^2);

思路三：

- B[i]=A[0]xA[1]xA[2]x...xA[i-1]xA[i+1]x...xA[n-1]可以看成时两部分的乘积
	- A[0]xA[1]xA[2]x...xA[i-1]
	- A[i+1]x...xA[n-1]
- 定义C[i] = A[0]xA[1]xA[2]x...xA[i-1], D[i] = A[i+1]x...xA[n-1]
- C[i] = C[i-1] x A[i-1];
- D[i] = D[i+1] x A[i+1];

## 3. 参考代码

//思路三参考代码
{% highlight c++ %}
void multiply(const vector<double>& array1, const vector<double>& array2) {
	int length1 = array1.size();
	int length2 = array2.size();

	if(length1 == length2 && length2 > 1) {
		array2[0] = 1;
		for(int i = 1; i < length1; i++) {
			array2 = array2[i-1] * array1[i-1];
		}

		double tmp = 1;
		for(int i = length2-2; i >= 0; i--) {
			tmp *= array1[i+1];
			array2[i] *= tmp;
		}
	}
}
{% endhighlight c++ %}

## 4. 思考

无；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)