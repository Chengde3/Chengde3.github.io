---
layout: post
title: 从上到下打印二叉树
date: 2015-08-18
categories: Algorithm
tags: algorithm tree
---

## 1. 问题描述

从上到下打印二叉树的每个结点，同一层次的结点按照从左到右的顺序打印。

## 2. 解题思路

使用队列存储打印的结点；每次把队列头部的元素打印出来

## 3. 参考代码

{% highlight c++ %}
struct BinaryTreeNode {
	int		m_nValue;
	BinaryTreeNode* m_pLeft;
	BinaryTreeNode* m_pRight;
};

void PrintFromTopToBottom(BinaryTreeNode* pTreeRoot) {
	if(!pTreeRoot) 
		return;

	std::deque<BinaryTreeNode *> dequeTreeNode;

	dequeTreeNode.push_back(pTreeRoot);

	while(dequeTreeNode.size()) {
		BinaryTreeNode* pNode = dequeTreeNode.front();
		dequeTreeNode.pop_front();

		printf("%d ", pNode->m_nValue);

		if(pNode->m_pLeft) 
			dequeTreeNode.push_back(pNode->m_pLeft);

		if(pNode->m_pRight)
			dequeTreeNode.push_back(pNode->m_pRight);
	}
}
{% endhighlight c++ %}

## 4. 思考

善用辅助数据结构；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)