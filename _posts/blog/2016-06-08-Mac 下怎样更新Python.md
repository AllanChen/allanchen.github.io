---
layout:     
title:      Mac下怎样系统的更新Python版本
category:
description: Mac下怎样系统的更新Python版本
---
1:下载最新的python 版本 [这里](https://www.python.org/download/releases/3.3.3)

2:安装下载好的文件

3:移动目录，系统的调用目录都在（/System/Library/Frameworks/Python.framework/Versions），把新装的python 移动的这个目录下面。
sudo mv /Library/Frameworks/Python.framework/Versions/3.3 /System/Library/Frameworks/Python.framework/Versions

4:改变Python安装目录的用户组为wheel
sudo chown -R root:wheel /System/Library/Frameworks/Python.framework/Versions/3.3

5:修改Python当前安装目录的符号链接
在 /System/Library/Frameworks/Python.framework/Versions/目录下有一个Current，这是一个目 录符号链接，指向当前的Python版本。原来指向2.7的，现在指向3.3。所以应先删除Current。然后重新建立Current符号链接，命令如 下：

sudo rm /System/Library/Frameworks/Python.framework/Versions/Current
sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.3 /System/Library/Frameworks/Python.framework/Versions/Current

