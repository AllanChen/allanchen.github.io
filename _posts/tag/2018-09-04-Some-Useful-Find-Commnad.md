---
layout: post
title: Useful find Command
category: tag
description: 35 条有用的find 命令
---

## Part I – Basic Find Commands for Finding Files with Names
1. Find Files Using Name in Current Directory
Find all the files whose name is tecmint.txt in a current working directory.
<pre class="prettyprint">
find . -name tecmint.txt
./tecmint.txt
</pre>

2. Find Files Under Home Directory
Find all the files under /home directory with name tecmint.txt.
<pre class="prettyprint">
find /home -name tecmint.txt
/home/tecmint.txt
</pre>

3. Find Files Using Name and Ignoring Case
Find all the files whose name is tecmint.txt and contains both capital and small letters in /home directory.
<pre class="prettyprint">
find /home -iname tecmint.txt
./tecmint.txt
./Tecmint.txt
</pre>


4. Find Directories Using Name
Find all directories whose name is Tecmint in / directory.
<pre class="prettyprint">
find / -type d -name Tecmint
/Tecmint
</pre>

5. Find PHP Files Using Name
Find all php files whose name is tecmint.php in a current working directory.
<pre class="prettyprint">
find . -type f -name tecmint.php
./tecmint.php
</pre>

6. Find all PHP Files in Directory
Find all php files in a directory.

<pre class="prettyprint">
find . -type f -name "*.php"
./tecmint.php
./login.php
./index.php
</pre>


## Part II – Find Files Based on their Permissions
7. Find Files With 777 Permissions
Find all the files whose permissions are 777.
<pre class="prettyprint">
find . -type f -perm 0777 -print
</pre>


8. Find Files Without 777 Permissions
Find all the files without permission 777.
<pre class="prettyprint">
find / -type f ! -perm 777
</pre>

9. Find SGID Files with 644 Permissions
Find all the SGID bit files whose permissions set to 644.
<pre class="prettyprint">
find / -perm 2644
</pre>

10. Find Sticky Bit Files with 551 Permissions
Find all the Sticky Bit set files whose permission are 551.
<pre class="prettyprint">
find / -perm 1551
</pre>

11. Find SUID Files
Find all SUID set files.
<pre class="prettyprint">
find / -perm /u=s
</pre>

12. Find SGID Files
Find all SGID set files.
<pre class="prettyprint">
find / -perm /g=s
</pre>

13. Find Read Only Files
Find all Read Only files.
<pre class="prettyprint">
find / -perm /u=r
</pre>

14. Find Executable Files
Find all Executable files.
<pre class="prettyprint">
find / -perm /a=x
</pre>

15. Find Files with 777 Permissions and Chmod to 644
Find all 777 permission files and use chmod command to set permissions to 644.
<pre class="prettyprint">
find / -type f -perm 0777 -print -exec chmod 644 {} \;
</pre>

16. Find Directories with 777 Permissions and Chmod to 755
Find all 777 permission directories and use chmod command to set permissions to 755.
<pre class="prettyprint">
find / -type d -perm 777 -print -exec chmod 755 {} \;
</pre>

17. Find and remove single File
To find a single file called tecmint.txt and remove it.
<pre class="prettyprint">
find . -type f -name "tecmint.txt" -exec rm -f {} \;
</pre>

18. Find and remove Multiple File
To find and remove multiple files such as .mp3 or .txt, then use.
<pre class="prettyprint">
find . -type f -name "*.txt" -exec rm -f {} \;
</pre>

<pre class="prettyprint">
find . -type f -name "*.mp3" -exec rm -f {} \;
</pre>

19. Find all Empty Files
To find all empty files under certain path.
<pre class="prettyprint">
find /tmp -type f -empty
</pre>


20. Find all Empty Directories
To file all empty directories under certain path.

<pre class="prettyprint">
find /tmp -type d -empty
</pre>

21. File all Hidden Files
To find all hidden files, use below command.
<pre class="prettyprint">
find /tmp -type f -name ".*"
</pre>

## Part III – Search Files Based On Owners and Groups
22. Find Single File Based on User
To find all or single file called tecmint.txt under / root directory of owner root.
<pre class="prettyprint">
find / -user root -name tecmint.txt
</pre>

23. Find all Files Based on User
To find all files that belongs to user Tecmint under /home directory.

<pre class="prettyprint">
find /home -user tecmint
</pre>

24. Find all Files Based on Group
To find all files that belongs to group Developer under /home directory.
<pre class="prettyprint">
find /home -group developer
</pre>

25. Find Particular Files of User
To find all .txt files of user Tecmint under /home directory.

<pre class="prettyprint">
find /home -user tecmint -iname "*.txt"
</pre>

## Part IV – Find Files and Directories Based on Date and Time

26. Find Last 50 Days Modified Files
To find all the files which are modified 50 days back.

<pre class="prettyprint">
find / -mtime 50
</pre>

27. Find Last 50 Days Accessed Files
To find all the files which are accessed 50 days back.

<pre class="prettyprint">
find / -atime 50
</pre>

28. Find Last 50-100 Days Modified Files
To find all the files which are modified more than 50 days back and less than 100 days.

<pre class="prettyprint">
find / -mtime +50 –mtime -100
</pre>

29. Find Changed Files in Last 1 Hour
To find all the files which are changed in last 1 hour.

<pre class="prettyprint">
find / -cmin -60
</pre>

30. Find Modified Files in Last 1 Hour
To find all the files which are modified in last 1 hour.

<pre class="prettyprint">
find / -mmin -60
</pre>

31. Find Accessed Files in Last 1 Hour
To find all the files which are accessed in last 1 hour.

<pre class="prettyprint">
find / -amin -60
</pre>

## Part V – Find Files and Directories Based on Size
32. Find 50MB Files
To find all 50MB files, use.

<pre class="prettyprint">
find / -size 50M
</pre>

33. Find Size between 50MB – 100MB
To find all the files which are greater than 50MB and less than 100MB.
<pre class="prettyprint">
find / -size +50M -size -100M
</pre>

34. Find and Delete 100MB Files
To find all 100MB files and delete them using one single command.

<pre class="prettyprint">
find / -size +100M -exec rm -rf {} \;
</pre>

35. Find Specific Files and Delete
Find all .mp3 files with more than 10MB and delete them using one single command.
<pre class="prettyprint">
find / -type f -name *.mp3 -size +10M -exec rm {} \;
</pre>

That’s it, We are ending this post here, In our next
article we will discuss more about other Linux commands in depth with practical examples. Let us know your opinions on this article using our comment section.

文章转自：https://www.tecmint.com/category/linux-commands/