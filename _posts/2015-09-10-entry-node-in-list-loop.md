---
layout: post
title: 链表中环的入口结点
date: 2015-09-10
categories: Algorithm
tags: algorithm list
---

## 1. 问题描述

一个链表中包含环，如何找出环的入口结点？

## 2. 解题思路

思路一：

- 设置一个快指针和一个慢指针，快指针一次走两步，慢指针一次走一步，若有环，快慢指针相遇于环中；
- 从相遇结点出发，一边走一边计数，再次回到相遇的结点的时候，得到环中结点的数目n；
- 设置两个指针p1,p2；p1走n步，然后两个指针同时走，两个指针相遇的地方即是环的入口结点；
- 因为p1,p2必然最后都在环中，且p1和p2相距n个结点，故必然在入口处相遇；

思路二：

- 设置快指针和慢指针，两个指针相遇表明有环；
- 此时让快指针回到链表的头部，快指针和慢指针同时走，且步伐相同；
- 两个指针相遇的结点即是环的入口；

## 3. 参考代码

//思路一参考代码
{% highlight c++ %}
struct ListNode {
	int m_pValue;
	ListNode* m_pNext;
};

//快慢指针的相遇结点；
ListNode* MeetingNode(ListNode* pHead) {
	if(pHead == NULL)
		return NULL;

	ListNode* pSlow = pHead->m_pNext;
	if(pSlow == NULL)
		return NULL;

	ListNode* pFast = pSlow->m_pNext;
	while(pFast != NULL && pSlow != NULL) {
		if(pFast == pSlow)
			return pFast;

		pSlow = pSlow->m_pNext;

		pFast = pFast->m_pNext;
		if(pFast != NULL)
			pFast = pFast->m_pNext;
	}
	return NULL;
}

ListNode* EntryNodeOfLoop(ListNode* pHead) {
	ListNode* meetingNode = MeetingNode(pHead);
	if(meetingNode == NULL)
		return NULL;

	//get the number of nodes in loop
	int nodesInLoop = 1;
	ListNode* pNode1 = meetingNode;
	while(pNode1->m_pNext != meetingNode) {
		pNode1 = pNode1->m_pNext;
		nodesInLoop++;
	}

	//move pNode1
	pNode1 = pHead;
	for(int i = 0; i < nodesInLoop; i++) {
		pNode1 = pNode1->m_pNext;
	}

	//move pNode1 and pNode2
	ListNode* pNode2 = pHead;
	while(pNode1 != pNode2) {
		pNode1 = pNode1->m_pNext;
		pNode2 = pNode2->m_pNext;
	}

	return pNode1;
}
{% endhighlight c++ %}

//思路二参考代码
{% highlight c++ %}
struct ListNode {
	int m_pValue;
	ListNode* m_pNext;
};

ListNode* find_loop(ListNode* pHead) {
	if(pHead == NULL)
		return NULL;

	ListNode* fast = pHead;
	ListNode* slow = pHead;
		
	//注意循环条件，保证下一个结点不为空；
	while(fast->m_pNext != NULL) {
		fast = fast->m_pNext->m_pNext;
		slow = slow->m_pNext;
		if(fast == slow)
			break;
	}

	if(fast->m_pNext == NULL)
		return NULL;

	slow = pHead;
	while(fast != slow) {
		fast = fast->m_pNext;
		slow = slow->m_pNext;
	}

	return fast;
}
{% endhighlight c++ %}

## 4. 思考

- 两种不同的解法，思路其实相似；注意如何证明；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)
- [2-5 求有环链表的环入口节点(证明及代码)](http://blog.csdn.net/jjdiaries/article/details/12882829)