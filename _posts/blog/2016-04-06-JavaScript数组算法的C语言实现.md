---
layout:     post
title:      JavaScript数组算法的C语言实现
category:   blog
description: JavaScript数组算法的C语言实现。
---
身为iOS 的leader最近“不务正业”的去了解了一下有关JS的底层，深有感触的想写一些有关JS数组底层的东西，所以这篇文章就出来了。。

最了几年的程序员，最大的体悟就是你要不断的学习，终生学习才不会让自己退步或者说是脱落。好吧，闲话不说直接进入主题吧。

大家接触的最多的js数组的操作无非就是“初始化，为空判断，追加元素，排序，逆序，插入元素，删除元素”下面我就把这些js数组的操作用C语言实现。

<pre class="prettyprint">
//
//  main.c
//  CTest
//
//  Created by ChanAllan on 3/25/15.
//  Copyright (c) 2015 ChanAllan. All rights reserved.
//

#include "<stdio.h>"
#include "<stdlib.h>"
#include "<malloc.h>"
//初始化数组
void init_arr (struct Arr* ,int);
//判断数组是否为空
boolean_t is_empty (struct Arr*);
//判断数组是否是满
boolean_t is_full  (struct Arr*);
//追加元素
boolean_t push (struct Arr* , int);
//正向排序
void sort (struct Arr*);
//逆序
void reverse(struct Arr*);
//插入元素
boolean_t insert(struct Arr*, int, int);
//删除元素（通过坐标）
boolean_t del(struct Arr*, int, int*);
//删除元素（通过元素）
boolean_t del_element(struct Arr *pArr, int element);
//打印数组
void show_arr(struct Arr*);

int main(int argc, const char * argv[]) {
    
    struct Arr arr;
    
    int val;
    
    init_arr(&arr, 6);
    show_arr(&arr);
    push(&arr, 1); 
    push(&arr, 2);
    push(&arr, 10);
    push(&arr, 20);
    push(&arr, 6);
    reverse(&arr);
    show_arr(&arr);
    sort(&arr);
    show_arr(&arr);
    insert(&arr, 3, 3);
    show_arr(&arr);
    del(&arr, 3, &val);
    show_arr(&arr);
    del_element(&arr, 1);
    show_arr(&arr);
    return 0;
}

</pre>

打印出来的结果是   
![打印结果](../../../../images/js-c/Screen Shot 2016-04-06 at 3.54.53 PM.png)

可能很多人会问，js本来就是一门脚本语言无语要了解太多的C，我会用js不是已经够了吗？这里我只想说一句：“你丫真的是Too Young Too Simple”, 程序=算法+数据结构 所以了解算法还是必要的！！