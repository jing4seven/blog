---
layout: post
title: "C语言中变量的内存分配"
description: "C语言中变量内存的分配"
category: C.and.Cpp
tags: [C,计算机基础]
---
{% include JB/setup %}

## 内存中的三个区域

* **栈**：存放函的数形参和函数内部的局部变量，空间由编译器自动分配，函数执行完毕后由编译器自动释放。

* **堆**：存放由动态分配函数（如malloc）请求分配的空间，必须使用free释放；如果忘记，会使所分配的空间一直被占用而导致内存泄漏。

* **具有外连接的、内部连接和空连接的静态变量的区域**

    * **全局区**：存放全局变量和静态变量。存在于程序整个运行期间，由编译器分配和释放。

    * **文字常量区**：存放文字常量。如char \*c = "123456"; 则"123456"为文字常量，存放在文字常量区，也有编译器分配和释放。

    * **程序代码区**：存放程序的二进制代码。


![Diagram1](/assets/images/c.alloc.diagram.png)

## 例子

    int main(int argc, char * argv[]) {
        int a;                  // 栈
        char s[] = "ac";        // s在栈， "ac"在文字常量区
        char *p1, *p2;          // p1, p2都在栈
        char *p3 = "123456";    // p3在栈， "123456"在文字常量区

        static int c = 0;           // c在全局区
        p1 = (char *)malloc(10);    // p1在栈，分配的10字节在堆
        p2 = (char *)malloc(20);    // 同p1
        strcpy(p1, "123456");       // "123465"在文字常量区

		free(p1);		// 手动释放请求的空间
		p1 = NULL;		// 讲指针重置为空
		free(p2);
		p2 = NULL;
		
        return 0;
    }
    
## 参考

1. 《深入理解计算机系统》 by Randal E. Bryant, David R.O Hallaren