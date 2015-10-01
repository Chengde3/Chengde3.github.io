---
layout: post
title: 合并两个排序的链表
date: 2015-08-14
categories: Algorithm
tags: algorithm list
---

## 1. 问题描述

输入两个递增排序的链表，合并着两个链表并使新链表中的结点仍然按照递增排序的。

## 2. 解题思路

两种思路：

- 设置两个指针分别指向两个链表，循环比较；
- 递归；

## 3. 参考代码

{% highlight c++ %}
struct ListNode{
	int m_nValue;
	ListNode* m_pNext;
};

ListNode* Merge(ListNode* pHead1, ListNode* pHead2) {
	//递归结束条件
	if(pHead1 == NULL) 
		return pHead2;
	else if(pHead2 == NULL) 
		return pHead1;

	ListNode* pMergedHead = NULL;

	if(pHead1->m_nValue < pHead2->m_nValue) {
		pMergedHead = pHead1;
		pMergedHead->m_pNext = Merge(pHead1->m_pNext, pHead2);
	} else {
		pMergedHead = pHead2;
		pMergedHead->m_pNext = Merge(pHead1, pHead2->m_pNext);
	}

	return pMergedHead;
}
{% endhighlight c++ %}

## 4. 思考

递归！递归！！递归！！！

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)