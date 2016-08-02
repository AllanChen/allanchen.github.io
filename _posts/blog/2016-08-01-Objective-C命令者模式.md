---
layout:     post
title:      Objective C--命令模式
category:   blog
description: 命令模式(Command)，将一个请求封装为一个对象，从而使你可用不同的请求对客户进行参数化；对请求排队或纪录请求日志，以及支持可撤销的操作。
---
今天想和大家分享的是命令模式。下面还和之前一样，先给出基本的定义。


> 
#### 命令模式(Command)，将一个请求封装为一个对象，从而使你可用不同的请求对客户进行参数化；对请求排队或纪录请求日志，以及支持可撤销的操作。

那么让我们简要的说一下命令模式的特点:
1. 它能比较容易地设计一个命令队列；
2. 在需要的情况下，可以较容易地将命令记入日志；
3. 允许接收请求的一方决定是否要否决请求；
4. 可以容易地实现对请求地撤销和重做；
5. 新的命令类不影响其他的类，因此增加新的命令类很容易；
6. 把请求一个操作的对象与知道怎么执行一个操作的对象分隔开；

**下面给出基本的类结构图。**
![基本类图结构](../../../../images/command-pattern/command-pattern.png)

**下面就根据上面的原理给出一个Demo:**

Receiver类：
<pre class="prettyprint">
#import <Foundation/Foundation.h>

@interface Receiver:NSObject
-(void)Action;
@end</pre>  

<pre class="prettyprint">
#import "Receiver.h"

@implementation Receiver
-(void)Action{
    NSLog(@"执行请求！");
}
@end</pre>  

Commands 类：
<pre class="prettyprint">
#import <Foundation/Foundation.h>

@class Receiver;
@interface Commands :NSObject{
    Receiver *myReceiver;
}
-(Commands*)MyInit:(Receiver*)receiver;
-(void)Execute;
@end</pre>  

<pre class="prettyprint">
#import "Commands.h"
#import "Receiver.h"

@implementation Commands
-(Commands*)MyInit:(Receiver *)receiver{
    myReceiver = receiver;
    return self;
}
-(void)Execute{
    return;
}
@end</pre>  

ConcreteCommands 类：
<pre class="prettyprint">
#import "Commands.h"

@class Receiver;
@interface ConcreteCommands :Commands
-(ConcreteCommands*)MyInit:(Receiver*)receiver;
@end
</pre>  

<pre class="prettyprint">
#import "ConcreteCommands.h"
#import "Receiver.h"

@implementation ConcreteCommands
-(ConcreteCommands*)MyInit:(Receiver *)receiver{
    myReceiver = receiver;
    return self;
}
-(void)Execute{
    [myReceiver Action];
}
@end
</pre>  

Invoker类：
<pre class="prettyprint">
#import <Foundation/Foundation.h>

@class Commands;
@interface Invoker :NSObject{
    Commands *myCommands;
}
-(void)SetCommands:(Commands*)commands;
-(void)ExecuteCommand;
@end
</pre>  

<pre class="prettyprint">
#import "Invoker.h"
#import "Commands.h"

@implementation Invoker
-(void)SetCommands:(Commands *)commands{
    myCommands = commands;
}
-(void)ExecuteCommand{
    [myCommands Execute];
}
@end
</pre>  

Main :
<pre class="prettyprint">
#import <Foundation/Foundation.h>
#import "Receiver.h"
#import "Commands.h"
#import "ConcreteCommands.h"
#import "Invoker.h"

int main(int argc,const char * argv[])
{
    @autoreleasepool{
        Receiver *r = [[Receiver alloc]init];
        Commands *c = [[ConcreteCommands alloc]MyInit:r];
        Invoker *i = [[Invoker alloc]init];
        [i SetCommands:c];
        [i ExecuteCommand];
    }
    return 0;
}
</pre>  




