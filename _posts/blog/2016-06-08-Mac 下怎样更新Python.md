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

