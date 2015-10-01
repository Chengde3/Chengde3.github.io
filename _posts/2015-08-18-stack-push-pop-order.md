---
layout: post
title: 栈的压入/弹出序列
date: 2015-08-18
categories: Algorithm
tags: algorithm stack
---

## 1. 问题描述

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出序列。

## 2. 解题思路

- 如果下一个要弹出的数字刚好时栈顶数字，那么直接弹出；
- 如果下一个要弹出的数字不再栈顶，把压栈序列中还没有入栈的数字压入辅助栈，直到把下一个需要弹出的数字压入栈顶为止。
- 如果所有的数字都压入了栈中，但是仍然没有找到下一个弹出的数字，那么该序列不是一个弹出序列；

## 3. 参考代码

{% highlight c++ %}
bool IsPopOrder(const int* pPush, const int* pPop, int nLength) {
	bool bPossible = false;

	if(pPush != NULL && pPop != NULL && nLength > 0) {
		const int* pNextPush = pPush;
		const int* pNextPop = pPop;

		//辅助栈
		std::stack<int> stackData;

		//出栈序列结束则循环结束
		while(pNextPop - pPop < nLength) {
			//栈顶元素不等于出栈元素
			while(stackData.empty() || stackData.top() != *pNextPop) {
				if(pNextPush - pPush == nLength) 
					break;

				stackData.push(*pNextPush);
				pNextPush++;
			}

			if(stackData.top() != *pNextPop)
				break;
			
			//出栈
			stackData.pop();
			pNextPop++;
		}

		if(stackData.empty() && pNextPop - pPop == nLength)
			bPossible = true;
	}

	return bPossible;
}
{% endhighlight c++ %}

## 4. 思考

无；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)