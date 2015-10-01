---
layout: post
title: 复杂链表的复制
date: 2015-08-19
categories: Algorithm
tags: algorithm list
---

## 1. 问题描述

请实现函数ComplexListNode* Clone(ComplexListNode* pHead)，复制一个复杂链表。在复杂链表中，每个结点除了有一个指向m_pNext指针指向下一个结点，还有一个m_pSibling指向链表的任意结点或者NULL。

## 2. 解题思路

思路一：

- 复制链表中的每一个结点，并用m_pNext链接起来；
- 设置指向每个结点的m_pSibling指针；

时间复杂度为O(n^2)，主要时间花费在定位m_pSibling上面；

思路二：

- 复制链表中的每一个结点N，并用m_pNext链接起来，同时创建新结点N‘，把<N,N'>的配对信息存放在hash表中；
- 设置m_pSibling指针，直接从hash表中查找即可；

时间复杂度为O(n)，空间复杂度为O(n)；

思路三：

- 复制链表中的每一个结点N，并用m_pNext链接起来，同时创建新结点N‘，同时把N'链接在N的后面；
- 设置m_pSibling指针，如果N的m_pSibling指向S，那么N'的m_pSibling指向S'。

时间复杂度为O(n)，空间复杂度为O(1)；

## 3. 参考代码

{% highlight c++ %}
struct ComplexListNode {
	int		m_nValue;
	ComplexListNode* m_pNext;
	ComplexListNode* m_pSibling;
};

void CloneNodes(ComplexListNode* pHead);
void ConnectSiblingNodes(ComplexListNode* pHead);
ComplexListNode* ReconnectNodes(ComplexListNode* pHead);

ComplexListNode* Clone(ComplexListNode* pHead) {
	CloneNodes(pHead);
	ConnectSiblingNodes(pHead);
	return ReconnectNodes(pHead);
}

//复制结点；并将结点附在原结点后面；
void CloneNodes(ComplexListNode* pHead) {
	ComplexListNode* pNode = pHead;

	while(pNode != NULL) {
		ComplexListNode* pCloned = new ComplexListNode();
		pCloned->m_nValue = pNode->m_nValue;
		pCloned->m_pNext = pNode->m_pNext;
		pCloned->m_pSibling = NULL;

		pNode->m_pNext = pCloned;
		pNode = pCloned->m_pNext;
	}
}

//设置m_pSibling结点；
void ConnectSiblingNodes(ComplexListNode* pHead) {
	ComplexListNode* pNode = pHead;

	while(pNode != NULL) { 
		ComplexListNode* pCloned = pNode->m_pNext;
		if(pNode->m_pSibling != NULL) {
			pCloned->m_pSibling = pNode->m_pSibling->m_pNext;
		}
		pNode = pCloned->m_pNext;
	}
}

//将两个链表拆分开来；
ComplexListNode* ReconnectNodes(ComplexListNode* pHead) {
	ComplexListNode* pNode = pHead;
	ComplexListNode* pClonedHead =	NULL;
	ComplexListNode* pClonedNode =	NULL;

	if(pNode != NULL) {
		pClonedHead = pClonedNode = pNode->m_pNext;
		pNode->m_pNext = pClonedNode->m_pNext;
		pNode = pNode->m_pNext;
	}

	while(pNode != NULL) {
		pClonedNode->m_pNext = pNode->m_pNext;
		pClonedNode = pClonedNode->m_pNext;

		pNode->m_pNext = pClonedNode->m_pNext;
		pNode = pNode->m_pNext;
	}
	return pClonedHead;
}
{% endhighlight c++ %}

## 4. 思考

暂无；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)