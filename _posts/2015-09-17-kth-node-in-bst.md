---
layout: post
title: 二叉搜索树的第k个结点
date: 2015-09-17
categories: Algorithm
tags: algorithm tree
---

## 1. 问题描述

给定一棵二叉搜索树，请找出其中的第k大的结点；

## 2. 解题思路

- 按照中序遍历的顺序遍历一棵二叉搜索树，遍历的值时递增排序的；

## 3. 参考代码

//递归代码
{% highlight c++ %}
#include<iostream>
using namespace std;

struct BinaryTreeNode {
	int m_nValue;
	BinaryTreeNode* m_pLeft;
	BinaryTreeNode* m_pRight;
};

BinaryTreeNode* kthNode(BinaryTreeNode* pRoot, unsigned int k) {
	if(pRoot == NULL || k == 0)
		return NULL;

	return KthNodeCore(pRoot, k);
}

BinaryTreeNode* KthNodeCore(BinaryTreeNode* pRoot, unsigned int &k) {
	BinaryTreeNode* target = NULL;
	if(pRoot->m_pLeft != NULL)
		target = KthNodeCore(pRoot->m_pLeft, k);

	if(target == NULL) {
		if(k == 1) 
			target = pRoot;
		k--;
	}

	if(target == NULL && pRoot->m_pRight != NULL)
		target = KthNodeCore(pRoot->m_pRight, k);

	return target;
}
{% endhighlight c++ %}

//非递归代码
{% highlight c++ %}
#include<iostream>
using namespace std;

struct BinaryTreeNode {
	int val;
	BinaryTreeNode* left;
	BinaryTreeNode* right;
};

BinaryTreeNode* KthNode(BinaryTreeNode* root, unsigned int k) {
	if(root == NULL || k <= 0)
		return NULL;

	stack<BinaryTreeNode*> s;
	BinaryTreeNode* p = root;

	while(p != NULL) {
		s.push(p);
		p = p->left;
	}

	while(!s.empty()) {
		BinaryTreeNode* currNode = s.pop();
		k--;
		if(k == 0)
			return currNode->val;
		if(currNode->right != NULL) {
			currNode = currNode->right;
			while(currNode != NULL) {
				s.push(currNode);
				currNode = currNode->left;
			}
		}
	}

	return NULL;
}
{% endhighlight c++ %}

## 4. 思考

注：非递归代码感觉更好理解一点；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)
- [Kth Smallest Element in a BST二叉搜索树的第k小结点](http://segmentfault.com/a/1190000003704692)