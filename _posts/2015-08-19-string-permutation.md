---
layout: post
title: 字符串的排列
date: 2015-08-19
categories: Algorithm
tags: algorithm string
---

## 1. 问题描述

输入一个字符串，打印出该字符串中字母的所有排列。

## 2. 解题思路

递归解决:

- 把第一个字符和后面所有的字符交换；
- 固定第一个字符，递归求后面所有字符的排列；

## 3. 参考代码

{% highlight c++ %}
void Permutation(char* pStr) {
	if(pStr == NULL)
		return;

	Permutation(pStr, pStr);
}

void Permutation(char* pStr, char* pBegin) {
	if(*pBegin == '\0')
		printf("%s\n", pStr);
	else {
		//注意此处的判断条件
		for(char* pCh = pBegin; *pCh != '\0'; pCh++) {
			char temp = *pCh;
			*pCh = *pBegin;
			*pBegin = temp;

			Permutation(pStr, pBegin + 1);

			//必须再交换回来；因为要保证是第一个字符和后面的每一个字符交换；
			temp = *pCh;
			*pCh = *pBegin;
			*pBegin = temp;
		}
	}
}
{% endhighlight c++ %}

## 4. 思考

无；

其他相关题目：

- [全排列全组合问题](http://blog.wangmingkuo.com/full-permutation/)
- [打印1到最大的n位数](http://blog.wangmingkuo.com/print-one-to-maxofndigits/)

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)