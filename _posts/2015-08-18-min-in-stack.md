---
layout: post
title: 包含min函数的栈
date: 2015-08-18
categories: Algorithm
tags: algorithm stack
---

## 1. 问题描述

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的min函数。在该栈中，调用min,push,pop的时间复杂度都是O(1)

## 2. 解题思路

定义一个辅助栈，做如下操作：

- 往数据栈中压入数据时，比较该数据A与辅助栈栈顶的元素B大小，如果A > B，则继续在辅助栈中压入最小元素；否则，压入数据A到辅助栈中；
- 从数据栈中pop数据时，同时也pop出辅助栈中的数据；

## 3. 参考代码

{% highlight c++ %}
//m_data是数据栈，m_min是辅助栈
template <typename T> void StackWithMin<T>::push(const T& value) {
	m_data.push(value);

	if(m_min.size() == 0 || value < m_min.top())
		m_min.push(value);
	//再次插入最小元素，保证两个栈大小相同；
	else
		m_min.push(m_min.top());
}

template <typename T> void StackWithMin<T>::pop() {
	assert(m_data.size() > 0 && m_min.size() > 0);

	m_data.pop();
	m_min.pop();
}

template <typename T> const T& StackWithMin<T>::min() const {
	assert(m_data.size() > 0 && m_min.size() > 0);

	return m_min.top();
}
{% endhighlight c++ %}

## 4. 思考

时间效率&&空间效率

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)