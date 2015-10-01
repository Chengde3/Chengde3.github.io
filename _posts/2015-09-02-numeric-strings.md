---
layout: post
title: 表示数值的字符串
date: 2015-09-02
categories: Algorithm
tags: algorithm
---

## 1. 问题描述

请实现一个函数用来判断字符串是否表示数值（包括整数和小数）.

## 2. 解题思路

- 首先看第一个字符是不是正负号；
- 如果是，在字符串上移动一个字符，继续扫描剩下的字符串0~9的数位；
- 如果是一个小数，则将遇到小数点。
- 如果是科学计数法表示的数值，在整数或者小数的后面还有可能遇到‘e'或者’E‘

## 3. 参考代码

{% highlight c++ %}
void scanDigits(char** string)
bool isExponential(char** string)
bool isNumeric(char* string) {
	if(string == NULL) 
		return false;

	if(*string == '+' || *string == '-') 
		++string;
	if(*string == '\0')
		return false;

	bool numeric = true;

	scanDigits(&string);
	if(*string != '\0') {
		//for floats
		if(*string == '.') {
			++string;
			scanDigits(&string);
			if(*string == 'e' || *string == 'E')
				numeric = isExponential(&string);
		} 
		// for integer
		else if(*string == 'e' || *string == 'E') 
			numeric = isExponential(&string);
		else 
			numeric = false;
	}
	return numeric && *string == '\0';
}

void scanDigits(char** string) {
	while(**string != '\0' && **string >= '0' && **string <= '9')
		++(*string);
}

bool isExponential(char** string) {
	if(**string != 'e' && **string != 'E')
		return false;

	++(*string);
	if(**string == '+' || **string == '-')
		++(*string);

	if(**string == '\0')
		return false;

	scanDigits(string);
	return (**string == '\0') ? true : false;
}
{% endhighlight c++ %}

## 4. 思考

无；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)