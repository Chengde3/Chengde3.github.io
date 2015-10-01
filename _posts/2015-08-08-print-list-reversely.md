---
layout: post
title: 从尾到头打印链表
date: 2015-08-08
categories: Algorithm
tags: algorithm list
---

## 1. 问题定义

输入一个链表的头节点，从尾到头反过来打印出每个节点的值；

## 2. 解题思路

在不改变链表结构的情况下，有如下三种思路

- 遍历链表，把节点存储在栈中；遍历完成之后，从栈顶输出；
- 使用递归算法（递归在本质上就是一个栈结构）；
- 使用动态数组vector（或者先遍历一遍，得到数组的大小）；

## 3. 参考代码

{% highlight c++ %}

#include<iostream>
#include<vector>
#include<stack>
using namespace std;

struct ListNode {
	int			m_nValue;
	ListNode*	m_pNext;
};

void PrintListReversingly_Iteratively(ListNode* pHead) {
	stack<ListNode*> nodes;
	
	ListNode* pNode = pHead;
	while(pNode != NULL) {
		nodes.push(pNode);
		pNode = pNode->m_pNext;
	}

	while(!nodes.empty()) {
		pNode = nodes.top();
		printf("%d\t", pNode->m_nValue);
		nodes.pop();
	}
}

void PrintListReversingly_Recursively(ListNode* pHead) {
	if(pHead != NULL) {
		if(pHead->m_pNext != NULL) {
			PrintListReversingly_Recursively(pHead->m_pNext);
		}
		printf("%d\t", pHead->m_nValue);
	}
}

void PrintListReversingly_UseVector(ListNode* pHead) {
	vector<int> value;

	ListNode* pNode = pHead;
	while(pHead != NULL) {
		value.push_back(pHead->m_nValue);
		pNode = pNode->m_pNext;
	}

	for(vector<int>::iterator iter = value.end(); iter != value.begin(); iter--) {
		printf("%d\t", *iter);
	}
}

{% endhighlight c++ %}

## 4. 注意事项

无

## 5. 参考文献

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)