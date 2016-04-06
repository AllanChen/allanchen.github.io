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
void init_arr (struct Arr *pArr ,int legth){
    pArr->pBase = (int *)malloc(sizeof(int ) * legth);
    if (NULL == pArr->pBase) {
        printf("动态内存分配失败！\n");
        exit(-1);
    }
    else{
        pArr->len = legth;
        pArr->cnt = 0;
    }
    return;
}

boolean_t is_empty (struct Arr *pArr){
    if (0 == pArr->cnt)
        return 1;
    else
        return 0;
}

boolean_t is_full  (struct Arr *pArr){
    if (pArr->cnt == pArr->len)
        return 1;
    else
        return 0;
}

void show_arr(struct Arr *pArr){
    if (is_empty(pArr)) {
        printf("数组为空\n");
    }
    else{
        for (int i=0; i<pArr->cnt; ++i) {
            printf("%d\n",pArr->pBase[i]);
        }
        printf("\n");
    }
}

boolean_t push (struct Arr *pArr , int val){
    if (is_full(pArr)) {
        return 0;
    }
    else{
        pArr->pBase[pArr->cnt] = val;
        (pArr->cnt)++;
        return 1;
    }
}
//最基本的冒泡算法
void sort (struct Arr *pArr){
    int i, j, t;
    for (i = 0; i<pArr->cnt; ++i) {
        for (j = i+1; j<pArr->cnt; ++j) {
            if (pArr->pBase[i] > pArr->pBase[j]) {
                t = pArr->pBase[i];
                pArr->pBase[i] = pArr->pBase[j];
                pArr->pBase[j] = t;
            }
        }
    }
}
void reverse(struct Arr *pArr){
    int t;
    int i=0;
    int j=pArr->cnt-1;
    
    while (i<j) {
        t = pArr->pBase[i];
        pArr->pBase[i] = pArr->pBase[j];
        pArr->pBase[j] = t;
        ++i;
        --j;
    }
    return;
}
boolean_t insert(struct Arr *pArr, int pos, int val){
    int i;
    if (is_full(pArr)) {
        return 0;
    }
    if (pos < 1 || pos>pArr->cnt+1) {
        return 0;
    }
    for (i = pArr->cnt-1; i>=pos-1; --i) {
        pArr->pBase[i+1] = pArr->pBase[i];
    }
    pArr->pBase[pos-1] = val;
    (pArr->cnt)++;
    return 1;

}
boolean_t del(struct Arr *pArr, int pos, int *val){
    int i;
    if (is_empty(pArr)) {
        return 0;
    }
    
    if (pos < 1 || pos > pArr->cnt) {
        return 0;
    }
    
    for (i=pos; i<pArr->cnt; ++i) {
        pArr->pBase[i-1] = pArr->pBase[i];
    }
    
    (pArr->cnt)--;
    return 1;
}

boolean_t del_element(struct Arr *pArr, int element){

    int i = 0;
    int pos = 0;
    int j = 0;
    
    for (i=0; i<pArr->cnt; ++i) {
        if (element == pArr->pBase[i]) {
            pos = i+1;
        }
    }
    
    for ( j = pos;j<pArr->cnt; ++j) {
        pArr->pBase[j-1] = pArr->pBase[j];
    }
    
    pArr->cnt --;
    return 1;
}
</pre>

打印出来的结果是   
![打印结果](../../../../images/js-c/Screen Shot 2016-04-06 at 3.54.53 PM.png)

可能很多人会问，js本来就是一门脚本语言无语要了解太多的C，我会用js不是已经够了吗？这里我只想说一句：“你丫真的是Too Young Too Simple”, 程序=算法+数据结构 所以了解算法还是必要的！！