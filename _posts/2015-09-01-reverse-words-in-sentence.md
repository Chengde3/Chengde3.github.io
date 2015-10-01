---
layout: post
title: 翻转单词的顺序
date: 2015-09-01
categories: Algorithm
tags: algorithm
---

## 1. 问题描述

输入一个英文句子，翻转句子中的单词的顺序，但单词内字符的顺序不变。为简单起见，标点符号和普通字母一样处理。例如输入的字符串为“I am a student.”,则输出为"student. a am I"

## 2. 解题思路

- 将整个字符串翻转；
- 将字符串中的单词翻转；

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

char* ReverseSentence(char* pData) {
	if(pData == NULL) 
		return NULL;

	char* pBegin = pData;
	char* pEnd = pData;
	while(*pEnd != '\0')
		pEnd++;
	//字符串结尾的字符不处理；
	pEnd--;

	//翻转整个句子
	Reverse(pBegin, pEnd);

	//翻转句子中的每个单词
	pBegin = pEnd = pData;
	while(*pBegin != '\0') {
		if(*pBegin == ' ') {
			pBegin++;
			pEnd++;
		} else if(*pEnd == ' ' || *pEnd == '\0') {
			Reverse(pBegin, --pEnd);
			pBegin = ++pEnd;
		} else 
			pEnd++;
	}
	return pData;
}
{% endhighlight c++ %}

## 4. 思考

- 厘清其中的逻辑；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)