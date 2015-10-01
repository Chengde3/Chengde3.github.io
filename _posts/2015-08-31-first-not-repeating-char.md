---
layout: post
title: 第一次只出现一次的字符
date: 2015-08-31
categories: Algorithm
tags: algorithm
---

## 1. 问题描述

在字符串中找出第一个只出现一次的字符。如输入“abaccdeff”，则输出‘b’

## 2. 解题思路

- 构建一个hashmap，key为字符，value为值出现的次数；统计hashmap即可；
- c++中没有实现hashmap,因字符char是一个长度为8的数据类型，因此总共有256种可能。创建一个长度为256的数组，每个字母根据其ASCII码值作为数组的下标对应数组的一个数字

## 3. 参考代码

{% highlight c++ %}
char FirstNotRepeatingChar(char* pString) {
	if(pString == NULL)
		return '\0';

	const int tableSize = 256;
	unsigned int hashTable[tableSize];
	for(unsigned int i = 0; i < 256; i++) 
		hashTable[i] = 0;

	char* pHashKey = pString;
	while(*pHashKey != '\0')
		hashTable[*(pHashKey++)]++;

	pHashKey = pString;
	while(*pHashKey != '\0') {
		if(hashTable[*pHashKey] == 1)
			return *pHashKey;

		pHashKey++;
	}

	return '\0';
}
{% endhighlight c++ %}

## 4. 思考

- 用数组模拟hashmap，用vector模拟栈等；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)