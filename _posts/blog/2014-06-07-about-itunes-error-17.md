---
layout:     post
title:      About iTunes ERROR 17
category:   blog
description: 关于在升级IOS系统是，iTunes Error 17 解决方法
---
## Mac 解决方法
* 贴上如下代码


    * ### Host Database#
    # localhost is used to configure the loopback interface
    # when the system is booting.  Do not change this entry.
    ##
    127.0.0.1	localhost
    255.255.255.255	broadcasthost
    ::1             localhost 
    fe80::1%lo0	localhost
    #127.0.0.1      osxdaily.com
    0.0.0.0		yahoo.com
    0.0.0.0		www.yahoo.com


* 如果系统版本是OS X 10.9时请清除缓存
<pre class="prettyprint">dscacheutil -flushcache;sudo killall -HUP mDNSResponder</pre>
##Windows 解决方法
* 直接编辑  C:\WINDOWS\system32\drivers\etc\hosts 
* 贴上如下代码
<pre class="prettyprint">
* ### Host Database#
# localhost is used to configure the loopback interface
# when the system is booting.  Do not change this entry.
##
127.0.0.1	localhost
255.255.255.255	broadcasthost
::1             localhost 
fe80::1%lo0	localhost
#127.0.0.1      osxdaily.com
0.0.0.0		yahoo.com
0.0.0.0		www.yahoo.com
</pre>