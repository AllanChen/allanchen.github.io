---
layout:     post
title:      How to create Private Pod
category:   blog
description: 如何创建一个自己的Pod,对于一些IOS 开发者而言，管理第三方库的确是一件令人头疼的事情。而Cocoapod 恰恰是解决你这个烦恼的一个第三方管理库。
---

对于一些IOS 开发者而言，管理第三方库的确是一件令人头疼的事情。而Cocoapod 恰恰是解决你这个烦恼的一个第三方管理库。
尽管pod上有许许多多的第三方库提供给开发者使用，但是很多人还是喜欢把自己的一些库或者Helper使用到各个项目上面去，这样不单单是可以提高个人的开发效率。对于以后有新人的加入，项目的重构管理起来都是颇为省劲。下面我就介绍一下如何去制作一个“私有的POD”。

### 创建一个Pod

* 创建一个Git的 [Repositories](https://github.com/new) 
* 创建一个 Podspec 
<pre class="prettyprint">pod spec create YOUR_PODSPEC_FILE_NAME</pre>
* 添加如下内容  [查看并复制](https://github.com/AllanChen/ACNetworkframework/blob/master/ACNetworkframework.podspec)
 
![Podspec File](https://raw.githubusercontent.com/AllanChen/allanchen.github.io/master/images/privatepod/Screen%20Shot%202014-07-08%20at%2010.01.15.png)
Podspec 文件解析：
1. s.name -- Pod 项目名字  
2. s.summary 一个简短的说明文档 （pod search命令就是根据这两项内容作为搜索文本的）  
3. s.homepage 库的主页，  
4. s.version 库代码的版本，  
5. s.license所采用的授权版本，  
6. s.author 是指作者。  
7. s.source 声明原代码的地址  
8. s.ios.deployment_target  
9. s.description 项目的描述  
10. s.source_files 项目的文件  
11. s.dependency 项目依赖的第三方库  
12. s.platform   支持的最低版本  
 
笔者在这个库中，用到的就是以上的一些属性。但是在PODSPEC 文件中，还有十分多的选项提供个大家去选择如

		# s.screenshots  = "www.example.com/screenshots_1.gif","www.example.com/screenshots_2.gif"
		# s.platform     = :ios
		# s.platform     = :ios, "5.0"
		# s.ios.deployment_target = "5.0"
		# s.osx.deployment_target = "10.7"  
		# s.public_header_files = "Classes/**/*.h"
		# s.resource  = "icon.png"
		# s.resources = "Resources/*.png"
		# s.preserve_paths = "FilesToSave", "MoreFilesToSave"
		# s.frameworks = "SomeFramework", "AnotherFramework"
		# s.library   = "iconv"
		# s.libraries = "iconv", "xml2"
		# s.requires_arc = true
		# s.xcconfig = { "HEADER_SEARCH_PATHS" => "$(SDKROOT)/usr/include/libxml2" }
		# s.dependency "JSONKit", "~> 1.4"

各种选项的意思其实在字义的表面已经可以看出来，我在这里就不一一细说。
创建好Podspec文件后，连同自己的代码一并上传到Git上面。

##### 本地的目录
![Local file](https://raw.githubusercontent.com/AllanChen/allanchen.github.io/master/images/privatepod/Screen%20Shot%202014-07-08%20at%209.55.53.png)

##### Git上面的目录
![Git file](https://raw.githubusercontent.com/AllanChen/allanchen.github.io/master/images/privatepod/Screen%20Shot%202014-07-08%20at%209.56.15.png)

### 需要注意的是，Podspec文件必须在git目录中！！
到这里，你已经很成功的创建了一个私有的Pod了。

### 使用你的Pod吧

在你使用该库的项目上创建Podfile 文件 ，添加如下内容，然后保存
<pre class="prettyprint"> platform :ios 
	pod 'YOUR_POD_NAME', :git => 'https://github.com/YOUR_POD_URL
</pre>

<pre class="prettyprint">pod install</pre>
![install Ing](https://raw.githubusercontent.com/AllanChen/allanchen.github.io/master/images/privatepod/Screen%20Shot%202014-07-08%20at%209.54.57.png)

### And more?
关于Pod的一些原理，大家可以看[这里](http://blog.devtang.com/blog/2014/05/25/use-cocoapod-to-manage-ios-lib-dependency/) 