---
layout: post
title: Mac Clear SVN Command
category: tag
description: Some Command
---
###清除Mac 项目中的.SVN文件

有时候因为一些SDK，和一些类库的不兼容。导致svn中的某些文件上传不了或者更新不了，这时候你就的清除这个文件下的svn文件，然后 iGnored

<pre class="prettyprint">find ./ -name ".svn" | xargs rm -Rf</pre>

