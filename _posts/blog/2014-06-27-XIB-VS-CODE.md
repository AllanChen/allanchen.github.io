---
layout:     
title:      XIB-VS-CODE
category:
description: XIB-VS-CODE
---
最近在不管在面试还是在项目的交流中，面试者和同事们都不约而同的提出问题。
究竟IOS的开发中，XIB是否真的有存在的必要吗？
Apple 的xib和storyBoard真的减轻了开发人员的开发成本吗？
Geek们真的愿意去用吗？

下面我们来比较一下，“纯手写UI+逻辑代码” 和 “通过XIB布局+逻辑代码” 两者的实用性和效率
我们以一个登录+展示列表 为功能点进行代码的编写

1：纯手写UI


2：通过XIB布局



总结：
通过比较，大家都不难发现。如果拿一些简单的布局来说，通过XIB开发者不但能够快速的构建自己需要的UI，还可以针对性的进行一些调整。而这是手写代码所做不到的一点。
而一旦如果你的元素太多的话，你的XIB文件就会变得越来大，渲染的速度也会相应的提高。所以在开发一些大型的应用软件或一些UI结构复杂的界面是，手写UI是比XIB要优秀。
写到这里，你可能会说。那就是纯手写比XIB要好咯。我可以肯定的回答---“不”！在我的角度我并不认为它们两是一定要独立存在的。XIB+手写代码，才是开发IOS效率和用户体验的王道。
