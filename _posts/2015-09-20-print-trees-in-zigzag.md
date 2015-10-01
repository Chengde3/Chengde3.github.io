---
layout: post
title: 按之字形顺序打印二叉树
date: 2015-09-20
categories: Algorithm
tags: algorithm tree
---

## 1. 问题描述

请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，以此类推；

## 2. 解题思路

使用两个栈来实现；

- 在打印某一层结点的时候，把下一层的子节点保存到相应的栈里；
- 如果当前打印的时奇数层，则先保存左子节点再保存右子节点；
- 如果当前打印的时偶数层，则先保存右子节点再保存左子节点；

## 3. 参考代码

{% highlight c++ %}
#include<iostream>
#include<stdio.h>
using namespace std;

struct BinaryTreeNode {
	int m_nValue;
	BinaryTreeNode* m_pLeft;
	BinaryTreeNode* m_pRight;
};

void Print(BinaryTreeNode* pRoot) {
	if(pRoot == NULL)
		return;

	stack<BinaryTreeNode*> levels[2];
	int current = 0;
	int next = 1;

	levels[current].push(pRoot);
	while(!levels[0].empty() || !levels[1].empty()) {
		BinaryTreeNode* pNode = levels[current].top();
		levels[current].pop();

		printf("%d ", pNode->m_nValue);

		if(current == 0) {
			if(pNode->m_pLeft != NULL)
				levels[next].push(pNode->m_pLeft);
			if(pNode->m_pRight != NULL)
				levels[next].push(pNode->m_pRight);
		} else {
			if(pNode->m_pRight != NULL)
				levels[next].push(pNode->m_pRight);
			if(pNode->m_pLeft != NULL) 
				levels[next].push(pNode->m_pLeft);
		}

		if(levels[current].empty()) {
			printf("\n");
			current = 1 - current;
			next = 1 - next;
		}
	}
}
{% endhighlight c++ %}

## 4. 思考

- 二叉树中的很多解法都需要使用栈或者队列，有时还可能不止一个；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)