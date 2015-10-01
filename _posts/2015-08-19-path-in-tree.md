---
layout: post
title: 二叉树中和为某一值的路径
date: 2015-08-19
categories: Algorithm
tags: algorithm tree
---

## 1. 问题描述

输入一棵二叉树和一个整数，打印出二叉树中结点值的和为输入整数的所有路径。从数的根结点开始往下一直到叶结点所经过的结点形成一条路径。

## 2. 解题思路

使用前序遍历二叉树的方法，具体如下：

- 访问某个结点，把该结点添加到路径上，并累加该结点的值；
- 如果是叶子结点 && 累加值等于输入的整数，则输出路径；
- 如果不是叶子结点，则递归访问它的子节点；
- 当前结点访问结束后，递归函数将自动回到它的父函数，因此需要在退出之前在路径上删除当前结点并减去当前结点的值；

## 3. 参考代码

{% highlight c++ %}
struct BinaryTreeNode {
	int		m_nValue;
	BinaryTreeNode* m_pLeft;
	BinaryTreeNode* m_pRight;
};

void FindPath(BinaryTreeNode* pRoot, int expectedSum) {
	if(pRoot ==	NULL)
		return;

	vector<int> path;
	int currentSum = 0;
	FindPath(pRoot, expectedSum, path, currentSum);
}

void FindPath(BinaryTreeNode* pRoot, int expectedSum, vector<int> path, int currentSum) {
	
	currentSum += pRoot->m_nValue;
	path.push_back(pRoot->m_nValue);

	//如果是叶子结点，并且路径上结点的和等于输入的值，打印这条路径
	bool isLeaf = pRoot->m_pLeft == NULL && pRoot->m_pRight == NULL;

	if(currentSum == expectedSum && isLeaf) {
		printf("A path is found: ");
		vector<int>::iterator iter = path.begin();
		for(; iter != path.end(); iter++)
			printf("%d\t", *iter);

		printf("\n");
	}

	//如果不是叶子结点，则遍历它的子结点
	if(pRoot->m_pLeft != NULL)
		FindPath(pRoot->m_pLeft, expectedSum, path, currentSum);
	if(pRoot->m_pRight != NULL)
		FindPath(pRoot->m_pRight, expectedSum, path, currentSum);

	//在返回父结点之前，在路径上删除当前结点，并在currentSum中减去相应的值;
	currentSum -= pRoot->m_nValue;
	path.pop_back();
}
{% endhighlight c++ %}

## 4. 思考

无；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)