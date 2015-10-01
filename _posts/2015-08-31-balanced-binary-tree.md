---
layout: post
title: 平衡二叉树
date: 2015-08-31
categories: Algorithm
tags: algorithm tree
---

## 1. 问题描述

输入一棵二叉树的根结点，判断该树是不是平衡二叉树。如果某二叉树中任意结点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树

## 2. 解题思路

思路一：

- 遍历每个结点，调用函数TreeDepth得到左右子树的深度，然后进行判断。需要重复遍历结点多次；

思路二：

- 采用后序遍历的方式遍历二叉树。在遍历到一个结点之前就已经遍历得到了它的左右子树。只要在遍历每个结点的时候记录它的深度，就可以一边遍历一边判断了。

## 3. 参考代码

//思路一参考代码
{% highlight c++ %}
struct BinaryTreeNode {
	int m_nValue;
	BinaryTreeNode* m_pLeft;
	BinaryTreeNode* m_pRight;
};

int IsBalanced(BinaryTreeNode* pRoot) {
	if(pRoot == NULL)
		return true;

	int left = TreeDepth(pRoot->m_pLeft);
	int right = TreeDepth(pRoot->m_pRight);
	int diff = left - right;
	if(diff > 1 || diff < -1)
		return false;

	return IsBalanced(pRoot->m_pLeft) && IsBalanced(pRoot->m_pRight);
}
{% endhighlight c++ %}

//思路二参考代码
{% highlight c++ %}
struct BinaryTreeNode {
	int m_nValue;
	BinaryTreeNode* m_pLeft;
	BinaryTreeNode* m_pRight;
};

int IsBalanced(BinaryTreeNode* pRoot, int* pDepth) {
	if(pRoot == NULL) {
		*pDepth = 0;
		return true;
	}

	int left, right;
	//如果左右子树都是平衡二叉树，判断合并之后是否是平衡二叉树；
	if(IsBalanced(pRoot->m_pLeft, &left) && (IsBalanced(pRoot->m_pRight, &right))) {
		int diff = left - right;
		if(diff <= 1 && diff >= -1) {
			*pDepth = 1 + (left > right ? left : right);
			return true;
		}
	}

	return false;
}

bool IsBalanced(BinaryTreeNode* pRoot) {
	int depth = 0;
	return IsBalanced(pRoot, &depth);
}
{% endhighlight c++ %}

## 4. 思考

二叉树啊二叉树。。。

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)