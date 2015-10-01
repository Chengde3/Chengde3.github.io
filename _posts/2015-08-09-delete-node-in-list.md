---
layout: post
title: 在O(1)时间删除链表节点
date: 2015-08-09
categories: Algorithm
tags: algorithm list
---

## 1. 问题定义

给定单向链表的头指针和一个结点指针，定义一个函数在O(1)时间删除该结点。

## 2. 解题思路

常规做法：

- 遍历链表，找到要删除结点的前一个结点，然后把这个结点的next指针指向下下个结点；

常规做法时间复杂度为O(n)，且如果没有给头节点，就无法完成操作；另一种思路是覆盖要删除结点的内容，具体如下。

另一种思路(假设要删除结点为i，i的下一个结点为j)：

- 把i的下一个结点j的内容复制给i，然后把i的指针指向j的下一个结点；然后删除结点j。
- 需要考虑如下两种情况：
	
	- 要删除的结点位于链表的尾部：遍历链表得到前序结点，删除该结点；
	- 链表中只有一个结点：在删除结点之后，需要把链表的头结点设置为NULL；
	
## 3. 参考代码

{% highlight c++ %}
struct ListNode {
	int m_nValue;
	ListNode* m_pNext;
};

void DeleteNode(ListNode** pListHead, ListNode* pToBeDeleted) {
	if(!pListHead || !pToBeDeleted) 
		return;

	//要删除的结点不是尾结点
	if(pToBeDeleted->m_pNext != NULL) {
		ListNode* pNext = pToBeDeleted->m_pNext;
		pToBeDeleted->m_nValue = pNext->m_nValue;
		pToBeDeleted->m_pNext = pNext->m_pNext;

		delete pNext;
		pNext = NULL;
	}

	//链表只有一个结点，删除头结点（也是尾结点）
	else if(*pListHead == pToBeDeleted) {
		delete pToBeDeleted;
		pToBeDeleted = NULL;
		*pListHead = NULL;
	}

	//链表中有多个结点，删除尾结点
	else {
		ListNode* pNode = *pListHead;
		while(pNode->m_pNext != pToBeDeleted) {
			pNode = pNode->m_pNext;
		}

		pNode->m_pNext = NULL;
		delete pToBeDeleted;
		pToBeDeleted = NULL;
	}
}
{% endhighlight c++ %}

## 4. 注意事项

删除不一定时常规意义上的删除，覆盖也是一种删除方式；

## 5. 参考文献

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)