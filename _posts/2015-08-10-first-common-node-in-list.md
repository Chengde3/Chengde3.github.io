---
layout: post
title: 两个链表的第一个公共结点
date: 2015-08-10
categories: Algorithm
tags: algorithm list
---

## 1. 问题定义

输入两个链表，找出他们的第一个公共结点。

## 2. 解题思路

思路一：

- 暴力法：依次遍历两个链表并比较；时间复杂度为O(mn)；

思路二：

- 把两个链表的结点压入两个栈中，然后比较两个栈栈顶元素是否相同，直到找到最后一个相同的结点，时间复杂度为O(m+n)，需要两个辅助栈；

思路三：

- 遍历两个链表得到长度n1,n2（假设n1 > n2）；
- 长链表走(n1-n2)步；
- 再同时遍历两个链表，找到第一个相同的结点；

## 3. 参考代码

{% highlight c++ %}
struct ListNode{
	int m_nKey;
	ListNode* m_pNext;
}

unsigned int GetListLength(ListNode* pHead);

ListNode* FindFirstCommonNode(ListNode* pHead1, ListNode* pHead2){

	//得到两个链表的长度;
	unsigned int nLength1 = GetListLength(pHead1);
	unsigned int nLength2 = GetListLength(pHead2);
	int nLengthDif = nLength1 - nLength2;

	ListNode* pListHeadLong = pHead1;
	ListNode* pListHeadShort = pHead2;
	if(nLength2 > nLength1) {
		pListHeadLong = pHead2;
		pListHeadShort = pHead1;
		nLengthDif = nLength2 - nLength1;
	}

	//先在长链表上走几步
	for(int i = 0; i < nLengthDif; i++) 
		pListHeadLong = pListHeadLong->m_pNext;

	//同时在两个链表上面遍历
	while((pListHeadLong != NULL) && (pListHeadShort != NULL) && (pListHeadShort != pListHeadLong)) {
		pListHeadLong = pListHeadLong->m_pNext;
		pListHeadShort = pListHeadShort->m_pNext;
	}

	//得到第一个公共结点
	ListNode* pFirstCommonNode = pListHeadLong;
	return pFirstCommonNode;
}

unsigned int GetListLength(ListNode* pHead) {
	ListNode* pNode = pHead;
	unsigned int nLength = 0;
	while(pNode != NULL) {
		++nLength;
		pNode = pNode->m_pNext;
	}
	return nLength;
}
{% endhighlight c++ %}


## 4. 思考

- 画图以辅助理解；
- 输入两个链表，如何确定长短链表？可以重新定义两个指针，比较两个链表的长度，将长链表头结点复制给其中一个指针即可；这样就可以区分两个长短链表了；

## 5. 参考文献

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)