---
layout: post
title: 用两个栈实现队列
date: 2015-08-08
categories: Algorithm
tags: algorithm queue stack
---

## 1. 问题定义

用两个栈实现一个队列。实现队列的两个函数appendTail和deleteHead，分别完成在队列尾部插入节点和在队列头部删除节点的功能；


## 2. 解题思路

通过具体的例子分析，同时通过画图的手段把问题形象化。可以得到如下思路，假设有两个栈stack1/stack2

- 插入元素：直接插入到stack1中；
- 删除元素：
	- 如果stack2为空，把stack1中的元素逐个弹出并压入stack2中。然后弹出栈顶元素；
	- 如果stack2不为空，则直接弹出栈顶元素；
	

## 3. 参考代码

{% highlight c++ %}
template<typename T> class CQueue {
	public:
		CQueue(void);
		~CQueue(void);

		void appendTail(const T& node);
		T deleteHead();

	private:
		stack<T> stack1;
		stack<T> stack2;
};

template<typename T> void CQueue<T>::appendTail(const T& element) {
	stack1.push(element);
}

template<typename T> T CQueue<T>::deleteHead() {
	if(stack2.size() <= 0) {
		while(stack1.size() > 0) {
			T& data = stack1.pop();
			stack2.push(data);
		}
	}

	if(stack2.size() == 0) {
		throw new exception("queue is empty");
	}

	T head = stack2.top();
	stack2.pop();

	return head;
}
{% endhighlight c++%}

## 4. 思考

通过具体的例子来分析复杂问题的思路很重要；

## 5. 扩展：用两个队列实现一个栈

思路类似。如下：假设有两个队列queue1/queue2

- 压栈：直接将元素存储在queue1中；
- 出栈：
	- 如果queue2为空，依次删除queue1中的元素病插入到queue2中，然后删除queue2中的一个元素即可；
	- 如果queue2不为空，直接删除queue2中的一个元素即可；

## 6. 参考文献

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)