---
layout: post
title: 二叉树的深度
date: 2015-08-31
categories: Algorithm
tags: algorithm tree
---

## 1. 问题描述

输入一棵二叉树的根结点，求该数的深度。从根节点到叶子结点依次经过的结点（含根/叶结点）形成树的一条路径，最长路径的长度为树的深度；

## 2. 解题思路

- 递归得到左右子树的深度，树的最大深度就是左右子树的深度+1；

## 3. 参考代码

{% highlight c++ %}
struct BinaryTreeNode {
	int m_nValue;
	BinaryTreeNode* m_pLeft;
	BinaryTreeNode* m_pRight;
};

int TreeDepth(BinaryTreeNode* pRoot) {
	if(pRoot == NULL)
		return 0;

	int nLeft = TreeDepth(pRoot->m_pLeft);
	int nRight = TreeDepth(pRoot->m_pRight);

	return (nLeft > nRight) ? (nLeft + 1) : (nRight + 1);
}
{% endhighlight c++ %}

## 4. 思考

二叉树啊二叉树。

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)