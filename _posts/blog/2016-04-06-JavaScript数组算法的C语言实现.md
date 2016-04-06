-'jia---da-
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

#include <stdio.h>
#include <stdlib.h>
#include <malloc/malloc.h>

void init_arr (struct Arr* ,int);
boolean_t is_empty (struct Arr*);
boolean_t is_full  (struct Arr*);
boolean_t push (struct Arr* , int);
void sort (struct Arr*);
void reverse(struct Arr*);
boolean_t insert(struct Arr*, int, int);
boolean_t del(struct Arr*, int, int*);
void show_arr(struct Arr*);
boolean_t del_element(struct Arr *pArr, int element);

int main(int argc, const char * argv[]) {
    
    struct Arr arr;
    
    int val;
    
    init_arr(&arr, 6);
//    show_arr(&arr);
    push(&arr, 4); // 在尾部追加元素
    push(&arr, 1);
//    push(&arr, -1);
    push(&arr, 10);
    push(&arr, 0);
    push(&arr, 6);
//    reverse(&arr);
//    sort(&arr);
    show_arr(&arr);
//    insert(&arr, 3, 3);
//    del(&arr, 3, &val);
    del_element(&arr, 1);
    show_arr(&arr);

</pre>
