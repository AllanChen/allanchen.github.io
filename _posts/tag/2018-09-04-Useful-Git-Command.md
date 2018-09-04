---
layout: post
title: Useful Git Command
category: tag
description: Git 常用命令
---

### 同步远程和本地目录
<pre class="prettyprint">
git init
git remote add origin $url_of_clone_source
git fetch origin
git checkout -b master --track origin/master # origin/master is clone's default
</pre>

### 展示远程的分支
<pre class="prettyprint">
git branch -a
</pre>

### 展示远程的仓库地址
<pre class="prettyprint">
git remote -v
</pre>

### reset
<pre class="prettyprint">
git reset --hard HEAD~1
</pre>

### stash
<pre class="prettyprint">
//stash files
git stash

//list all stash
git stash list

//apply near stash
git stash apply

//apply index stash
git stash apply --index
</pre>

### 设置你的邮箱
<pre class="prettyprint">
git config --global user.name "Allan Chan"
git config --global user.email "allan@example.com"
</pre>




