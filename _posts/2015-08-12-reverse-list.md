---
layout: post
title: 反转链表
date: 2015-08-12
categories: Algorithm
tags: algorithm list
---

## 1. 问题描述

定义一个函数，输入一个链表的头结点，反转该链表并输出反转后链表的头结点。

## 2. 解题思路

定义三个结点：

- 前一个结点
- 当前结点
- 后一个结点

然后调整指针即可

## 3. 参考代码

{% highlight c++ %}
ListNode* ReverseList(ListNode* pHead) {

	ListNode* pReverseHead = NULL;
	ListNode* pNode = pHead;
	ListNode* pPre = NULL;

	while(pNode != NULL) {
		ListNode* pNext = pNode->m_pNext;

		//尾结点
		if(pNext == NULL) {
			pReverseHead = pNode;
		}

		pNode->m_pNext = pPre;
		pPre = pNode;
		pNode = pNext;
	}
	return pReverseHead;
}
{% endhighlight c++ %}

## 4. 思考

需要考虑特殊的测试用例：

- 链表头指针是NULL；
- 输入的链表只有一个结点等；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)