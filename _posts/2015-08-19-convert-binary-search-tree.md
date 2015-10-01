---
layout: post
title: 二叉搜索树与双向链表
date: 2015-08-19
categories: Algorithm
tags: algorithm tree list
---

## 1. 问题描述

输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的双向链表。要求不能创建任何新的结点，只能调整树中结点指针的指向；

## 2. 解题思路

按照中序递归遍历的思路；

- 当遍历转换到根结点时，它的左子树已经转换成一个排序的链表了，并且处于链表中的最后一个结点是当前结点的最大值，将其与根节点链接起来；
- 然后遍历转换右子树，并把根节点和右子树中最小的结点链接起来；

## 3. 参考代码

{% highlight c++ %}
struct BinaryTreeNode {
	int		m_nValue;
	BinaryTreeNode* m_pLeft;
	BinaryTreeNode* m_pRight;
};

void ConvertNode(BinaryTreeNode* pNode, BinaryTreeNode** pLastNodeInList);

BinaryTreeNode* Convert(BinaryTreeNode* pRootOfTree) {
	//排序链表中的最后一个结点
	BinaryTreeNode* pLastNodeInList = NULL;
	ConvertNode(pRootOfTree, &pLastNodeInList);

	//pLastNodeInList指向双向链表的尾结点，需要返回头节点；
	BinaryTreeNode* pHeadOfList = pLastNodeInList;
	while(pHeadOfList != NULL && pHeadOfList->m_pLeft != NULL) {
		pHeadOfList = pHeadOfList->m_pLeft;
	}

	return pHeadOfList;
}

void ConvertNode(BinaryTreeNode* pNode, BinaryTreeNode** pLastNodeInList) {
	if(pNode == NULL) 
		return;

	BinaryTreeNode* pCurrent = pNode;

	//递归左子树
	if(pNode->m_pLeft != NULL) 
		ConvertNode(pCurrent->m_pLeft, pLastNodeInList);

	//合并根结点和左子树链表
	pCurrent->m_pLeft = *pLastNodeInList;
	if(*pLastNodeInList != NULL)
		(*pLastNodeInList)->m_pRight = pCurrent;

	//链表合并之后，根结点变成了最后一个结点;
	*pLastNodeInList = pCurrent;

	//递归右子树
	if(*pNode->m_pRight != NULL) 
		ConvertNode(pCurrent->m_pRight, pLastNodeInList);
}
{% endhighlight c++ %}

## 4. 思考

递归！递归！！递归！！！

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)