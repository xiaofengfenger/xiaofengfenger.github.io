---
layout: post
title: 面试遇到的问题总结集合
description: 在找工作过程中遇到的一些技术问题和对于面试方法的总结
tag: 面试
---
### 指针和引用的区别
指针是一个变量，只不过这个变量存储的是一个地址，指向内存的一个存储单元,而引用跟原来的变量实质上是同一个东西，只不过是原变量的一个别名而已  
`int a=1;int *p=&a;  
int a=1;int &b=a;`  
上面定义了一个整形变量和一个指针变量p，该指针变量指向a的存储单元，即p的值是a存储单元的地址。  
而下面2句定义了一个整形变量a和这个整形a的引用b，事实上a和b是同一个东西，在内存占有同一个存储单元。  
(2)可以有const指针，但是没有const引用；  
(3)指针可以有多级，但是引用只能是一级（`int **p；合法 而 int &&a是不合法的`）  
(4)指针的值可以为空，但是引用的值不能为NULL，并且引用在定义的时候必须初始化；  
(5)指针的值在初始化后可以改变，即指向其它的存储单元，而引用在进行初始化后就不会再改变了。  
(6)"sizeof引用"得到的是所指向的变量(对象)的大小，而"sizeof指针"得到的是指针本身的大小；  
(7)指针和引用的自增(++)运算意义不一样；

### DNS协议的作用
DNS，简单地说，就是Domain Name System，翻成中文就是“域名系统”。  
在一个TCP/IP架构的网络（例如Internet）环境中，DNS是一个非常重要而且常用的系统。  
主要的功能就是将人易于记忆的Domain Name与人不容易记忆的IP Address作转换。  

“头文件中的 #ifndef/#define/#endif 防止该头文件被重复引用”  
其实“被重复引用”是指一个头文件在同一个cpp文件中被include了多次，这种错误常常是由于include嵌套造成的。  
比如：存在a.h文件#include "c.h"而此时b.cpp文件导入了#include "a.h" 和#include "c.h"此时就会造成c.h重复引用。  
下面给一个#ifndef/#define/#endif的格式：  

 #ifndef A_H意思是"if not define a.h"  如果不存在a.h  
 接着的语句应该#define A_H  就引入a.h  
 最后一句应该写#endif   否则不需要引入

### 二叉树遍历
遍历即将树的所有结点访问且仅访问一次。按照根节点位置的不同分为前序遍历，中序遍历，后序遍历。  

前序遍历：根节点->左子树->右子树  
中序遍历：左子树->根节点->右子树  
后序遍历：左子树->右子树->根节点  

http://wx2.sinaimg.cn/small/e9563fcfly1fkf8s6z3z8j206m076glg.jpg  

前序遍历：abdefgc  
中序遍历：debgfac  
后序遍历：edgfbca  

数据结构：一般以链表存储树  
    typedef char datatype;  

    typedef struct BinNode{  
        datatype data;  
        struct BinNode* lchild;  
        struct BinNode* rchild;  
    }BinNode;  

    typedef BinNode* bintree;          //bintree本身是个指向结点的指针  

递归实现(以前序遍历为例，其他的只是输出的位置（printf函数的位置）稍有不同)  
    void preorder(bintree t){  
            if(t){  
                printf("%c ",t->data);  
                preorder(t->lchild);  
                preorder(t->rchild);  
            }  
    }


### C/C++申请空间与释放空间的两种方法  
1、C语言的函数malloc和free  
     函数malloc和free在头文件<stdlib.h>中什声明  
     `void * malloc(size_t size)`     动态配置内存，大小有size决定，返回值成功时为任意类型指针，失败时为NULL。   
     `void  free(void *ptr)`        释放动态申请的内存空间，调用free()后ptr所指向的内存空间被收回，如果ptr指向未知地方或者指向的空间已被收回，则会发生不可预知的错误，如果ptr为NULL，free不会有任何作用。  

  malloc函数动态申请的内存空间是在堆里(而一般局部变量存于栈里)，并且该段内存不会被初始化，与全局变量不一样，如果不采用手动free()加以释放，则该段内存一直存在，直到程序退出才被系统回收，所以为了合理使用内存，在不使用该段内存时，应该调用free()释放。另外，如果在一个函数里面使用过malloc，最好要配对使用free，否则容易造成内存泄露（没有将内存还给自由存储区）。  

2、C++中的运算符new和delete  
      new和delete是C++中的运算符，不是库函数，不需要库的支持，同时，他们是封装好的运算符  

new是动态分配内存的运算符，自动计算需要分配的空间，在分配类类型的内存空间时，同时调用类的构造函数，对内存空间进行初始化，即完成类的初始化工作。动态分配内置类型是否自动初始化取决于变量定义的位置，在函数体外定义的变量都初始化为0，在函数体内定义的内置类型变量都不进行初始化。

delete是撤销动态申请的内存运算符。delete与new通常配对使用，与new的功能相反，可以对多种数据类型形式的内存进行撤销，包括类，撤销类的内存空间时，它要调用其析构函数，完成相应的清理工作，收回相应的内存资源。




 本篇文章会不断更新后续的问题...
