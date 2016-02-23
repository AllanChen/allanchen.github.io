---
layout:     post
title:      Cocoapods with Xcode 6 and Yosemite
category:   blog
description: 所以说NO ZUO NO DIE 对于一些急着体验的Yosemite系统的朋友来说，在新的系统上有太多的不兼容了，不过对于苹果的设计。我个人还是给予满分。
---
COCOSPODS 就是其中一个不兼容，你的更新xcode，COCOSPODS 才可以继续用pod install

具体步奏如下

* 打开 Xcode 6
* Command + ,
* 选择 Locations
* 将 Command Line Tools version 变为 Xcode 6.0
* 卸载 cocospods
 
* <pre class="prettyprint">$ sudo gem uninstall cocoapods</pre>
* 安装 xcodeproj

* <pre class="prettyprint">$ sudo gem install xcodeproj</pre> 
* 安装 cocoapods 
 
<pre class="prettyprint">
$ sudo gem install cocoapods
</pre>

* Run pod --version to verify that it worked

执行上面的命令之后，可能你还会失败。但是不要紧，把你Terminal的窗口关掉重新cd到你的项目在执行pod install就可以了。