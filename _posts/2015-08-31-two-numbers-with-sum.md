---
layout: post
title: 	和为s的两个数字
date: 2015-08-31
categories: Algorithm
tags: algorithm
---

## 1. 问题描述

输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得他们的和正好是s。如果有多对数字的和等于s，输出任意一对即可；

扩展题目：

输入两个整数n和m，从数列1,2,3......n中随意取几个数，使其和为m，要求将其中所有的可能组合列出来；

## 2. 解题思路

- 设置两个指针，ahead，behind，分别指向数组的头和尾；
- 计算两个指针指向的数字的和，如果和等于s，则找到；
- 如果和大于s，则后面的指针向前移动一位；
- 如果和小于s，则前面的指针向后移动一位；

## 3. 参考代码

{% highlight c++ %}
bool FindNumbersWithSum(int data[], int length, int sum, int* num1, int* num2) {
	bool found = false;
	if(length < 1 || num1 == NULL || num2 == NULL)
		return found;

	int ahead = length - 1;
	int behind = 0;
	while(ahead > behind) {
		long long curSum = data[ahead] + data[behind];

		if(curSum == sum) {
			*num1 = data[behind];
			*num2 = data[ahead];
			found = true;
			break;
		} else if(curSum > sum)
			ahead--;
		else 
			behind++;
	}

	return found;
}
{% endhighlight c++ %}

//扩展题代码
{% highlight c++ %}
#include<list>
#include<iostream>
using namespace std;

list<int> list1;
void find_factor(int sum, int n) {

	//递归出口
	if(n <= 0 || sum <= 0)
		return;

	//输出所有找到的结果
	if(sum == n) {
		//反转list
		list1.reverse();
		for(list<int>::iterator iter = list1.begin(); iter != list1.end(); iter++)
			cout << *iter << "+";
		cout << n << endl;
		list1.reverse();
	}

	list1.push_front(n);
	find_factor(sum-n, n-1);	//放n，n-1个数填满sum-n
	list1.pop_front();
	find_factor(sum, n-1);		//不放n,n-1个数填满sum
}

int main() {
	int sum = 100;
	int n = 50;

	find_factor(sum, n);
	return 0;
}
{% endhighlight c++ %}

## 4. 思考

- 如果需要输出所有的对，该如何解决？（借助hashmap？）；

## 5. 参考

- [和为S的两个数字VS和为s的连续正数序列](http://www.cnblogs.com/heyonggang/p/3642455.html)
- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)