---
layout: post
title: 左旋字符串
date: 2015-09-01
categories: Algorithm
tags: algorithm
---

## 1. 问题描述

字符串的左旋操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串的左旋转操作。比如输入字符串“abcdefg”和数字2，该函数将返回左旋转2位得到的结果“cdefgab”

## 2. 解题思路

参考旋转单词的思路，可以得到如下思路：

- 根据数字将字符串分成两部分，前一部分含有n个字符；
- 分别翻转两个部分的字符串；
- 翻转整个字符串；

## 3. 参考代码

{% highlight c++ %}
void Reverse(char* pBegin, char* pEnd) {
	if(pBegin == NULL || pEnd == NULL) 
		return;

	while(pBegin < pEnd) {
		char tmp = *pBegin;
		*pBegin = *pEnd;
		*pEnd = tmp;

		pBegin++;
		pEnd--;
	}
}

char* LeftRotateString(char* pStr, int n) {
	if(pStr != NULL) {
		int nLength = static_cast<int>(strlen(pStr));
		if(nLength > 0 && n > 0 && n < nLength) {
			char* pFirstStart = pStr;
			char* pFirstEnd = pStr + n - 1;
			char* pSecondStart = pStr + n;
			char* pSecondEnd = pStr + nLength - 1;

			//翻转字符串的前面n个字符
			Reverse(pFirstStart, pFirstEnd);
			//翻转字符串的后面部分
			Reverse(pSecondStart, pSecondEnd);
			//翻转整个字符串
			Reverse(pFirstStart, pSecondEnd);
		}
	}

	return pStr;
}
{% endhighlight c++ %}

## 4. 思考

无；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)