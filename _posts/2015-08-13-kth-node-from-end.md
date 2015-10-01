---
layout: post
title: 链表中倒数第k个结点
date: 2015-08-13
categories: Algorithm
tags: algorithm list
---

## 1. 问题描述

输入一个链表，输出该链表中的倒数第k个结点。

## 2. 思路描述

两种解题思路

- 遍历链表得到链表长度，从头结点向后走n-k+1步，需要遍历链表两次；
- 设置两个指针，一个指针先走k-1步，另一个指针在头节点不动，然后两个指针同时走，第一个指针到达尾结点的时候，第二个指针即是倒数第k个结点；

## 3. 参考代码

{% highlight c++ %}
struct ListNode {
	int m_nValue;
	ListNode* m_pNext;
};

ListNode* FindKthToTail(ListNode* pListHead, unsigned int k) {
	//空指针判断
	if(pListHead == NULL || k == 0) 
		return NULL;

	ListNode* pAhead = pListHead;
	ListNode* pBehind = NULL;

	for(unsigned int i = 0; i < k - 1; i++) {
		//如果链表结点数小于k-1
		if(pAhead->m_pNext != NULL)
			pAhead = pAhead->m_pNext;
		else
			return NULL;
	}

	pBehind = pListHead;
	while(pAhead->m_pNext != NULL) {
		pAhead = pAhead->m_pNext;
		pBehind = pBehind->m_pNext;
	}

	return pBehind;
}
{% endhighlight c++ %}

## 4. 注意事项

此题不难，关键在于考虑到特殊输入，如：

- 输入链表为空；
- k为0；
- 结点数量比k小；

其次，对于链表的题目，当我们用一个指针不能解决问题的时候，可以尝试**使用两个指针来遍历链表**。可以让其中的一个指针遍历的速度快一些，或者让它先在链表一走若干步；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)