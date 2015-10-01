---
layout: post
title: 二叉树的镜像
date: 2015-08-14
categories: Algorithm
tags: algorithm tree
---

## 1. 问题描述

请完成一个函数，输入一个二叉树，该函数输出它的镜像

## 2. 解题思路

递归

## 3. 参考代码

{% highlight c++ %}
struct BinaryTreeNode {
	int		m_nValue;
	BinaryTreeNode* m_pLeft;
	BinaryTreeNode* m_pRight;
};

void MirrorRecursively(BinaryTreeNode* pNode) {
	//递归结束条件
	if(pNode == NULL)
		return;
	if(pNode->m_pLeft == NULL && pNode->m_pRight ==	NULL) 
		return;

	BinaryTreeNode* temp = pNode->m_pLeft;
	pNode->m_pLeft = pNode->m_pRight;
	pNode->m_pRight = temp;

	if(pNode->m_pLeft != NULL)
		MirrorRecursively(pNode->m_pLeft);
	if(pNode->m_pRight != NULL)
		MirrorRecursively(pNode->m_pRight);
}
{% endhighlight c++ %}

## 4. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)