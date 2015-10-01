---
layout: post
title: 删除链表中重复的结点
date: 2015-09-11
categories: Algorithm
tags: algorithm list
---

## 1. 问题描述

在一个排序的链表中，如何删除重复的结点？（把重复的结点全部删除）

## 2. 解题思路

- 确定删除函数的参数，因为头节点也可能被删除，因此函数申明应该用指针的指针；
- 如果当前结点的值和下一个结点的值相同，那么它们就是重复结点，需要删除；
- 把当前结点的前一个结点和后面值比当前结点要大的结点相连；

## 3. 参考代码

{% highlight c++ %}
struct ListNode {
	int m_nValue;
	ListNode* m_pNext;
}

void deleteDuplication(ListNode** pHead) {
	if(pHead == NULL || *pHead == NULL)
		return;

	ListNode* pPreNode = NULL;
	ListNode* pNode = *pHead;
	while(pNode != NULL) {
		ListNode* pNext = pNode->m_pNext;
		bool needDelete = false;
		if(pNext != NULL && pNext->m_nValue == pNode->m_nValue)
			needDelete = true;

		if(!needDelete) {
			pPreNode = pNode;
			pNode = pNode->m_pNext;
		} else {
			int value = pNode->m_nValue;
			ListNode* pToBeDel = pNode;
			while(pToBeDel != NULL && pToBeDel->m_nValue == value) {
				pNext = pToBeDel->m_pNext;

				delete pToBeDel;
				pToBeDel = NULL;

				pToBeDel = pNext;
			}

			if(pPreNode == NULL)
				*pHead = pNext;
			else 
				pPreNode->m_pNext = pNext;
			pNode = pNext;
		}
	}
}
{% endhighlight c++ %}

## 4. 思考

- 由于头节点可能会被删除，因此需要指针的指针，也就是所指向头节点的指针的值可能会改变，但是指向头节点指针的指针的值则不会改变，画个图就能很清晰地看出来；
- 注意其中的逻辑处理，以及代码实现；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)