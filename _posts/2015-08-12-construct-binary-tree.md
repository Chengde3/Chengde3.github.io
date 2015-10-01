---
layout: post
title: 重建二叉树
date: 2015-08-12
categories: Algorithm
tags: algorithm tree
---

## 1. 问题描述

输入二叉树的前序遍历和中序遍历的结果，重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复数字。

## 2. 解题思路

- 根据**前序遍历序列**的第一个数字创建根结点；
- 在**中序遍历序列**中找到根节点的位置；确定左右子树结点的数量；
- 递归构建左右子树；

## 3. 参考代码

{% highlight c++ %}
struct BinaryTreeNode {
	int			m_nValue;
	BinaryTreeNode* m_pLeft;
	BinaryTreeNode* m_pRight;
};

BinaryTreeNode* Construct(int* preorder, int* inorder, int length) {
	if(preorder == NULL || inorder == NULL || length == 0) 
		return NULL;

	return ConstructCore(preorder, preorder + length - 1, inorder, inorder + length - 1);
}

BinaryTreeNode* ConstructCore(int* startPreorder, int* endPreorder, int* startInorder, int* endInorder) {
	
	//前序的第一个结点为root
	int rootValue = startPreorder[0];
	BinaryTreeNode* root = new BinaryTreeNode();
	root->m_nValue = rootValue;
	root->m_pLeft = NULL;
	root->m_pRight = NULL;

	//递归结束条件
	if(startPreorder == endPreorder) {
		//考虑无效输入
		if(startInorder == endInorder && *startPreorder == *startInorder)
			return root;
		else 
			throw std::exception("Invalid input.");
	}

	//在中序遍历中找到根结点的值
	int* rootInorder = startInorder;
	while(rootInorder <= endInorder && *rootInorder != rootValue)
		++rootInorder;

	//无效输入
	if(rootInorder == endInorder && *rootInorder != rootValue) 
		throw std::exception("Invalid input.");

	int leftLength = rootInorder - startInorder;
	int* leftPreorderEnd = startPreorder + leftLength;
	if(leftLength > 0) {
		//构建左子树
		root->m_pLeft = ConstructCore(startPreorder + 1, leftPreorderEnd, startInorder, rootInorder - 1);
	}

	if(leftLength < endPreorder - startPreorder) {
		//构建右子树
		root->m_pRight = ConstructCore(leftPreorderEnd + 1, endPreorder, rootInorder + 1, endInorder);
	}

	return root;
}
{% endhighlight c++ %}

## 4. 思考

需要考虑异常输入以及如何递归；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)