---
layout: post
title: AFNetworking ＋ NSOperation 如何管理耦合的网络请求
category: blog
description: 在应用程序的开发当中，网络请求无疑是最常接触的一块。各种的数据传输，回报，变更无一不跟网络打交道。而在此当中有一些请求是非常依赖于上一个请求放回出来的结果的。例如：我们想收集一个用户最新的资料（包括：头像，地址，姓名等等。），必须想让他跟新一下信息或者重新通过第三方的平台授权后再去上报资料。这一系列的操作都是非常常见的。而在iOS 的开发中，无疑最常用的框架就是 AFNetWorking. 这次我就结合这个框架简单演示下如何做一个有耦合行单网络请求。
---

在应用程序的开发当中，网络请求无疑是最常接触的一块。各种的数据传输，回报，变更无一不跟网络打交道。而在此当中有一些请求是非常依赖于上一个请求放回出来的结果的。   

例如：我们想收集一个用户最新的资料（包括：头像，地址，姓名等等。），必须想让他跟新一下信息或者重新通过第三方的平台授权后再去上报资料。这一系列的操作都是非常常见的。而在iOS 的开发中，无疑最常用的框架就是 AFNetWorking. 这次我就结合这个框架简单演示下如何做一个有耦合行单网络请求。

> 所用框架：AFNetworking ~>2.4

### Demo
<pre class="prettyprint lang-html">
<code>
- (void)updateUserInfoAndPostToServer{
    NSString *updateUserInfo = @"...";
    NSString *postUserInfo = @"...";

    AFHTTPSessionManager *manager = [AFHTTPSessionManager manager];

    NSOperationQueue *queue = [[NSOperationQueue alloc] init];
    queue.name = @"AFHTTPSessionManager queue for User Update";
    NSOperation *completionOperation = [NSBlockOperation blockOperationWithBlock:^{
        NSLog(@"All done");
    }];

    NSOperation *updateOperation = [AFHTTPSessionOperation operationWithManager:manager HTTPMethod:@"GET" URLString:urlString1 parameters:nil uploadProgress:nil downloadProgress:nil success:^(NSURLSessionDataTask *task, id responseObject) {
        NSLog(@"update success");
    } failure:^(NSURLSessionDataTask *task, NSError *error) {
        NSLog(@"update faile failed 1 - error = %@", error.localizedDescription);
    }];
    [completionOperation addDependency:updateOperation];

    NSOperation *postUserInfoOperation = [AFHTTPSessionOperation operationWithManager:manager HTTPMethod:@"GET" URLString:urlString2 parameters:nil uploadProgress:nil downloadProgress:nil success:^(NSURLSessionDataTask *task, id responseObject) {
        NSLog(@"postUserInfoOperation success");
    } failure:^(NSURLSessionDataTask *task, NSError *error) {
        NSLog(@"postUserInfoOperation  - error = %@", error.localizedDescription);
    }];
    [completionOperation addDependency:postUserInfoOperation];

    [queue addOperations:@[updateOperation, postUserInfoOperation] waitUntilFinished:false];
    [[NSOperationQueue mainQueue] addOperation:completionOperation];  

    //在这个请求完成之后，你就可以update 一下主线程上的UI 了。
}
</code>
</pre>
