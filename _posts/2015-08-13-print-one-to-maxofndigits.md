---
layout: post
title: 打印1到最大的n位数
date: 2015-08-13
categories: Algorithm
tags: algorithm
---

## 1. 问题描述

输入数字n，按顺序打印从1到最大的n位十进制数。

## 2. 解题思路

需要考虑大数的情况；

两种解题思路如下：

- 此时可以在字符串中模拟数字加法；
- 可以看成全排列问题；递归求解；

## 3. 参考代码

### 3.1 常规解法

{% highlight c++ %}
bool Increment(char* number);
void PrintNumber(char* number);

void Print1ToMaxOfNDigits(int n) {
	if(n <= 0)
		return;

	char *number = new char[n+1];
	memset(number, '0', n);
	number[n] = '\0';

	while(!Increment(number)) 
		PrintNumber(number);

	delete []number;
}

bool Increment(char* number) {
	bool isOverflow = false;
	//进位标识
	int nTakeOver = 0;
	int nLength = strlen(number);

	for(int i = nLength - 1; i >= 0; i--) {
		int nSum = number[i] - '0' + nTakeOver;
		//最高位加1
		if(i == nLength -1)
			nSum ++;

		if(nSum >= 10) {
			//如果最高位加1后大于10
			if(i == 0)
				nTakeOver = false;
			else {
				//处理进位
				nSum -= 10;
				nTakeOver = 1;
				number[i] = '0' + nSum;
			}
		} else {
			number[i] = '0' + nSum;
			break;
		}
	}
	return isOverflow;
}

void PrintNumber(cha* number) {
	bool isBeginning0 = true;
	int nLength = strlen(number);

	for(int i = 0; i < nLength; i++) {
		if(isBeginning0 && number[i] != '0')
			isBeginning0 = false;

		if(!isBeginning0)
			printf("%c", number[i]);
	}
	printf("\t");
}
{% endhighlight c++ %}

### 3.2 递归解法

{% highlight c++ %}
//把问题转换成数字排列，递归解决
void Print1ToMaxOfNDigits(int n) {
	if(n < 0)
		return;

	char* number = new char[n+1];
	number[n] = '\0';

	for(int i = 0; i < 10; i++) {
		number[0] = i + '0';
		Print1ToMaxOfNDigitsRecursively(number, n, 0);
	}

	delete[] number;
}

void Print1ToMaxOfNDigitsRecursively(char* number, int length, int index) {
	if(index == length - 1) {
		PrintNumber(number);
		return;
	}

	for(int i = 0; i < 10; i++) {
		number[index+1] = i + '0';
		Print1ToMaxOfNDigitsRecursively(number, length, index + 1);
	}
}
{% endhighlight c++ %}

## 4. 思考

- 类似的问题还有大数的加法/减法/乘法/除法/阶层等等；
- 字符串时一个简单，有效的大数表示方法；



## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)