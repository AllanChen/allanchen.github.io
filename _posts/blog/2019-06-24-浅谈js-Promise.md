---
layout: post
title: 浅谈 JavaScript Promise
category: blog
description: 浅谈 JavaScript Promise
---
浅谈 JavaScript Promise

## Promise.all
官方解析：方法用于将多个 Promise 实例，包装成一个新的 Promise 实例

通俗解析：它以数组形式所谓参数接受多个promise 实例，__且当所有传入的promise 执行完成后，返回一个新的promise__。
下面我们来看看代码：

``` Javascript
function task1(){
    var p = new Promise(function(resolve, reject){
        //异步操作1
        setTimeout(function(){
            console.log('task1执行完成');
            resolve('task1 return data');
        }, 1000);
    });
    return p;            
}
function task2(){
    var p = new Promise(function(resolve, reject){
        //异步操作2
        setTimeout(function(){
            console.log('task2执行完成');
            resolve('task2 return data');
        }, 2000);
    });
    return p;            
}
function task3(){
    var p = new Promise(function(resolve, reject){
        //异步操作3
        setTimeout(function(){
            console.log('task3执行完成');
            resolve('task3 return data');
        }, 2000);
    });
    return p;            
}

Promise.all(task1(), task2(), task3()).then(function(result){
  console.log(result);
})

```

Promise.all 其实是提供了一个并行执行的异步操作的能力。在Promise.all 中所有异步操作完成后才会进行回调。

通过这个例子可以看到，其实promise.all 的适用场景很多，比如支付，同步请求等场景。
[参考代码](https://codesandbox.io/s/promise-all-and-race-code-b5l9d)

## Promise.race

官方解析：该方法接一个迭代器(如数组等), 返回一个新的Promise对象. 只要迭代器中有一个Promise对象状态改变(被实现或被拒绝), 那么返回的Promise将以相同的值被实现或拒绝, 然后它将忽略迭代器中其他Promise的状态变化。

通俗解析：Promise.race 它以一个数据作为接收参数，参数里面的方法谁先完成就回调谁。不知道这样子说各位看官会不会更加容易理解。
下面我们来看看代码：

``` javascript
function task1(){
    var p = new Promise(function(resolve, reject){
        //异步操作1
        setTimeout(function(){
            console.log('task1执行完成');
            resolve('task1 return data');
        }, 1000);
    });
    return p;            
}
function task2(){
    var p = new Promise(function(resolve, reject){
        //异步操作2
        setTimeout(function(){
            console.log('task2执行完成');
            resolve('task2 return data');
        }, 2000);
    });
    return p;            
}
function task3(){
    var p = new Promise(function(resolve, reject){
        //异步操作3
        setTimeout(function(){
            console.log('task3执行完成');
            resolve('task3 return data');
        }, 2000);
    });
    return p;            
}

Promise.race([task1(), task2(), task3()]).then(function(result){
  console.log(result);
}).catch(function (resason){
  console.log(resason)
})
```

[参考代码](https://codesandbox.io/s/promise-all-and-race-code-b5l9d)



## Promise.reject
官方解析：用于改变该Promise本身的状态为拒绝, 执行后, 将触发 then | catch的onRejected回调, 并把reject的参数传递给onRejected回调。

通俗解析：接受Promise 中失败的状态。
下面我们来看看代码：

```javascript
function testReject() {
  var p = new Promise(function(resolve, reject) {
    setTimeout(function() {
      console.log("excuting restReject function");
      reject("Failed");
    }, 1000);
  });

  return p;
}

testReject().then(
      function(result) {
        console.log("then resolve");
      },
      function(result, data) {
        console.log("then reject");
        console.log(result);
        // console.log(data);
      }
    );
```

## Promise.catch
官方解析：用于您的promise组合中的错误处理

通俗解析：捕获Promise  中错误错误处理, 包括error reject 等

用心的看官看到这里可能会有疑问，then 里面不是也可以捕获错误吗，这个方法跟那个有什么不一样？
catch 方法对于我们来说更像是一种报错机制，下面我们来看看代码

```javascript
function testResolve() {
  var p = new Promise(function(resolve, reject) {
    setTimeout(function() {
      console.log("excuting testResolve function");
      resolve("success");
    }, 1000);
  });
  return p;
}

testResolve().then(function(result){
  console.log(result);
  console.log(errorFunctionCall());
}).catch(function(reason){
  	console.log("rejected");
    console.log(reason);
})
```

上面代码很清晰的可以看到，当出现js 异常时会进入catch 这个方法来捕获，这样就不会报错卡死js。
catch 方法和我们的try/catch 的方法相似。

[参考代码](https://codesandbox.io/s/promise-reolve-and-reject-code-ccelc)


## Promise.resolve
官方解析：用于改变该Promise本身的状态为实现, 执行后, 将触发then的onFulfilled回调, 并把resolve的参数传递给onFulfilled回调

通俗解析：resolve 你可以简单理解问在Promise 执行成功的时候要进行回调的一个方法（虽然这么说好像有点不正确，希望有读者可以提供更通俗的解析）
下面我们来看看代码：

```javascript
function testResolve() {
  var p = new Promise(function(resolve, reject) {
    setTimeout(function() {
      console.log("excuting testResolve function");
      resolve("success");
    }, 1000);
  });
  return p;
}

testResolve().then(function(result){
  console.log(result);
})
```

在上面代码中，可以很清晰的看到，resolve 几乎可以等同与在promise 执行成功后进行的一次回调。可能有读者这时候有疑问，那如果我有多个状态的成功组合在一次才进行回调，这怎么办？下面我们来介绍一下then 的链式操作。

我们来举例一个现实场景来理解这个链式操作可能会更好，比如：有天，你需要做一个功能是现实一个用户的资料，但是这个用户的资料是来自于3个接口的,这时候链式操作就可以派上用场。
下面我们来看看代码：

```javascript
function getUserInfo() {
  var p = new Promise(function(resolve, reject) {
    // var resultData = $.get("https:///getuserdata");
    var resultData = { id: 1, name: "allan", phone: "10086" };
    resolve(resultData);
  });
  return p;
}
function getUserWeightAndBirthday(userData) {
  var p = new Promise(function(resolve, reject) {
    // var resultData = $.get("https:///getuserdata");
    var resultData = { weight: "50kg", birthday: "2000-01-01" };
    const userWeightAndBirthday = Object.assign({}, userData, resultData);
    resolve(userWeightAndBirthday);
  });
  return p;
}
function combineUserInfo(userInfo) {
  var p = new Promise(function(resolve, reject) {
    var resultData = {
      img: "https:www.allanhost.com/allan.png",
      address: "GZ"
    };
    const combineUserInfoData = Object.assign({}, resultData, userInfo);
    resolve(combineUserInfoData);
  });
  return p;
}

// then chain
 getUserInfo()
   .then(function(userNameAndPhone) {
     return getUserWeightAndBirthday(userNameAndPhone);
   })
   .then(function(userinfo) {
     return combineUserInfo(userinfo);
   })
   .then(function(userInfo) {
     console.log(userInfo);
   });
```

[参考代码](https://codesandbox.io/s/promise-reolve-and-reject-code-ccelc)

