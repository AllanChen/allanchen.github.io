---
layout:     post
title:      浅谈GCD
category:   blog
description: 要理解 GCD ，你要先熟悉与线程和并发相关的几个概念。这两者都可能模糊和微妙，所以在开始 GCD 之前先简要地回顾一下它们。
---
## iOS GCD 基础名词解析:

### 串行与并行

串行和并行都是相对于队列而言的 -队列（负责调度任务）  
串行队列：一个接一个的调度任务  
并发队列：可以同时调度多个任务

### 同步与异步

串行与并行针对的是队列，而同步与异步，针对的则是线程。 最大的区别在于，同步线程要阻塞当前线程，必须要等待同步线程中的任务执行完，返回以后，才能继续执行下一任务；而异步线程则是不用等待。 仅凭这几句话还是很难理解，所以可以多准备几个案例，边分析边理解。

**串行与并行针对的是队列，而同步与异步，针对的则是线程。**

### GCD API
<pre class="prettyprint">
dispatch_sync(..., ^(block)) // 同步线程
dispatch_async(..., ^(block)) // 异步线程

Serial Dispatch Queue，这叫做串行队列

Concurrent Dispatch Queue，叫做并行队列

// 全局队列，一个特殊的并行队列  
dispatch_get_global_queue

// 主队列，在主线程中运行，因为主线程只有一个，所以这是一个特殊的串行队列
dispatch_get_main_queue

// 从DISPATCH_QUEUE_SERIAL看出，这是串行队列
dispatch_queue_create("com.demo.serialQueue", DISPATCH_QUEUE_SERIAL)

// 同理，这是一个并行队列  
dispatch_queue_create("com.demo.concurrentQueue", DISPATCH_QUEUE_CONCURRENT)

// 线程延迟执行
dispatch_time_t 创建时间 

double delayInSeconds = 1.0;
dispatch_time_t popTime = dispatch_time(DISPATCH_TIME_NOW,(int64_t)(delayInSeconds * NSEC_PER_SEC)); // 延迟一秒
dispatch_after(popTime, dispatch_get_main_queue(), ^(void){
//Code Here
});

</pre>

## 相关术语：

### Dispatch Groups（调度组）

Dispatch Group 会在整个组的任务都完成时通知你。这些任务可以是同步的，也可以是异步的，即便在不同的队列也行。而且在整个组的任务都完成时，Dispatch Group 可以用同步的或者异步的方式通知你。因为要监控的任务在不同队列，那就用一个 dispatch_group_t 的实例来记下这些不同的任务。

### Critical Section 临界区

就是一段代码不能被并发执行，也就是，两个线程不能同时执行这段代码。这很常见，因为代码去操作一个共享资源，例如一个变量若能被并发进程访问，那么它很可能会变质（译者注：它的值不再可信）。

### Concurrency vs Parallelism 并发与并行

并发和并行通常被一起提到，所以值得花些时间解释它们之间的区别。

并发代码的不同部分可以“同步”执行。然而，该怎样发生或是否发生都取决于系统。多核设备通过并行来同时执行多个线程；然而，为了使单核设备也能实现这一点，它们必须先运行一个线程，执行一个上下文切换，然后运行另一个线程或进程。这通常发生地足够快以致给我们并发执行地错觉，如下图所示：

![](https://camo.githubusercontent.com/55145c5a8cf3d6f840e7267acd550869f92becfe/687474703a2f2f63646e312e72617977656e6465726c6963682e636f6d2f77702d636f6e74656e742f75706c6f6164732f323031342f30312f436f6e63757272656e63795f76735f506172616c6c656c69736d2e706e67)

虽然你可以编写代码在 GCD 下并发执行，但 GCD 会决定有多少并行的需求。并行要求并发，但并发并不能保证并行。

更深入的观点是并发实际上是关于构造。当你在脑海中用 GCD 编写代码，你组织你的代码来暴露能同时运行的多个工作片段，以及不能同时运行的那些。如果你想深入此主题，看看 [这个由Rob Pike做的精彩的讲座 。](http://vimeo.com/49718712)

## 例子

### 同步线程死锁
<pre class="prettyprint">
NSLog(@"Task 1"); 
dispatch_sync(dispatch_get_main_queue(), ^{
    NSLog(@"Task 2");
});
NSLog(@"Task 3");
</pre>

**代码解析：**  
1. dispatch_sync表示是一个同步线程  
2. dispatch_get_main_queue表示运行在主线程中的主队列  
3. "Task2" 是同步线程的任务  
4. Task3 需要等待"Task2"结束之后再执行  
 **所以最终的结果只会打印“Task 1”，这就是同步线程死锁。**