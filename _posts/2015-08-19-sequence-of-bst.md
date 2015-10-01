---
layout: post
title: 二叉搜索树的后序遍历序列
date: 2015-08-19
categories: Algorithm
tags: algorithm tree
---

## 1. 问题描述

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果时则返回true，否则返回flase。假设输入的数组的任意两个数字都互不相同；

## 2. 解题思路

[二叉搜索树](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%85%83%E6%90%9C%E5%B0%8B%E6%A8%B9)的左子树的结点 <= 根结点 <= 右子树的结点

- 确定根结点；
- 遍历数组，前面比根节点元素小的元素都是左子树的结点；
- 遍历数组，如果后面的元素有比根节点小的元素，返回false；
- 递归判断左右子树是否是二叉搜索树；

## 3. 参考代码

{% highlight c++ %}
struct BinaryTreeNode {
	int		m_nValue;
	BinaryTreeNode* m_pLeft;
	BinaryTreeNode* m_pRight;
};

bool VerifySequenceOfBST(int sequence[], int length) {
	if(sequence == NULL || length == 0)
		return false;

	int root = sequence[length-1];

	//在二叉搜索树中左子树的结点小于根结点
	int i = 0;
	for(; i < length-1; ++i) {
		if(sequence[i] > root)
			break;
	}

	//在二叉搜索树中右子树的结点大于根结点
	int j = i;
	for(; j < length-1; j++) {
		if(sequence[i] < root)
			return false;
	}

	//判断左子树是不是二叉搜索树
	bool left = true;
	if(i > 0) 
		left = VerifySequenceOfBST(sequence, i);

	//判断右子树是不是二叉搜索树
	bool right = true;
	if(i < length - 1) 
		right = VerifySequenceOfBST(sequence+i, length-i-1);

	return (left && right);
}
{% endhighlight c++ %}

## 4. 思考

递归！递归！！递归！！！

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)