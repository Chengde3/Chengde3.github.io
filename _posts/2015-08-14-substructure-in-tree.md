---
layout: post
title: 树的子结构
date: 2015-08-14
categories: Algorithm
tags: algorithm tree
---

## 1. 问题描述

输入两颗二叉树A和B，判断B是不是A的子结构。

## 2. 解题思路

- 在树A中找到和树B的根节点的值一样的结点R；
- 判断树A中以R为根结点的子树是不是包含和树B一样的结构；

## 3. 参考代码

{% highlight c++ %}
bool DoesTree1HaveTree2(BinaryTreeNode* pRoot1, BinaryTreeNode* pRoot2);
bool HasSubTree(BinaryTreeNode* pRoot1, BinaryTreeNode* pRoot2) {
	bool result = false;

	if(pRoot1 != NULL && pRoot2 != NULL) {
		if(pRoot1->m_nValue == pRoot2->m_nValue)
			result = DoesTree1HaveTree2(pRoot1, pRoot2);
		//如果找到了，就不需要继续找了
		if(!result) 
			result = HasSubTree(pRoot1->m_pLeft, pRoot2);
		if(!result)
			result = HasSubTree(pRoot1->m_pRight, pRoot2);
	}
	return result;
}

bool DoesTree1HaveTree2(BinaryTreeNode* pRoot1, BinaryTreeNode* pRoot2) {
	//递归结束条件
	if(pRoot2 == NULL) 
		return true;
	if(pRoot1 == NULL) 
		return false;
	if(pRoot1->m_nValue != pRoot2->m_nValue)
		return false;

	return DoesTree1HaveTree2(pRoot1->m_pLeft, pRoot1->m_pRight) && DoesTree1HaveTree2(pRoot2->m_pLeft, pRoot2->m_pRight);
}
{% endhighlight c++ %}

## 4. 思考

- 递归！递归！！递归！！！
- 循环！循环！！循环！！！

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)