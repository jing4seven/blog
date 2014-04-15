---
layout: post
title: "memory alloc in c"
description: ""
category: 
tags: []
---
{% include JB/setup %}



### 例子
	int a;  // 栈
	char s[] = "ac"; // s在栈， "ac"在文字常量区
	char *p1, *p2; // p1, p2都在栈
	char *p3 = "123456"; // p3在栈， "123456"在文字常量区
	static int c = 0; // c在全局区
	p1 = (char *)malloc(10);  // p1在栈，分配的10字节在堆
	p2 = (char *)malloc(20); // 同p1
	strcpy(p1, "123456"); // "123465"在文字常量区



That's a test!
