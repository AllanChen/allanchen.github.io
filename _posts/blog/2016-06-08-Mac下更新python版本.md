---
layout:     post
title:      Mac下怎样系统的更新Python版本
category:   blog
description: Mac下怎样系统的更新Python版本
---
1:下载最新的python 版本 [这里](https://www.python.org/download/releases/3.3.3)

2:安装下载好的文件

3:移动目录，系统的调用目录都在（/System/Library/Frameworks/Python.framework/Versions），把新装的python 移动的这个目录下面。

<pre class="prettyprint">
sudo mv /Library/Frameworks/Python.framework/Versions/3.3 /System/Library/Frameworks/Python.framework/Versions
</pre>

4:改变Python安装目录的用户组为wheel
<pre class="prettyprint">
sudo chown -R root:wheel /System/Library/Frameworks/Python.framework/Versions/3.3
</pre>

5:修改Python当前安装目录的符号链接
在 /System/Library/Frameworks/Python.framework/Versions/目录下有一个Current，这是一个目 录符号链接，指向当前的Python版本。原来指向2.7的，现在指向3.3。所以应先删除Current。然后重新建立Current符号链接，命令如 下：
<pre class="prettyprint">
sudo rm /System/Library/Frameworks/Python.framework/Versions/Current
</pre>

<pre class="prettyprint">
sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.3 /System/Library/Frameworks/Python.framework/Versions/Current
</pre>

第6步：删除旧的命令符号链接

在/usr/bin目录下有4个python命令的符号链接，使用下面的命令先删除

<pre class="prettyprint">
sudo rm /usr/bin/pydoc
sudo rm /usr/bin/python
sudo rm /usr/bin/pythonw
sudo rm /usr/bin/python-config
</pre>

第7步：重新建立新的命令符号链接
将第6步删除的符号链接重新使用下面命令建立，它们都指向Python3.3了。
sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.3/bin/pydoc3.3 /usr/bin/pydoc
sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.3/bin/python3.3 /usr/bin/python
sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.3/bin/pythonw3.3 /usr/bin/pythonw
sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.3/bin/python3.3m-config /usr/bin/python-config

第8步：更新/root/.bash_profile文件中的路径
cd ~
 vim .bash_profile 

在.bash_profile插入下面的内容即可

#### Setting PATH for Python 3.3
#### The orginal version is saved in .bash_profile.pysave
PATH="/System/Library/Frameworks/Python.framework/Versions/3.3/bin:${PATH}"
export PATH

