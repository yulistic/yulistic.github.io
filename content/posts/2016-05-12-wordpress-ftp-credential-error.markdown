---
author: yulistic
comments: true
date: 2016-05-12 06:49:06+00:00
type: post
link: http://yulistic.com/?p=95
slug: wordpress-ftp-credential-error
title: '[Wordpress] FTP credential error'
wordpress_id: 95
language:
- English
topics:
- Issues
---

**In a word
**Check whether the owner of wordpress directory is the same as that of web server process (_i.e._ apache or nginx).

**Problem**
I cannot update plugins or theme in wordpress because of FTP credential failure.

**Reason**
It might occur because of diverse reasons. In my case, it is because of a permission mismatch between the owner of nginx service (substitute of apache) and the owner of wordpress directory.
When you are trying to update wordpress stubs in administrator web page, _nginx (or apache/daemon if you use apache),_ the owner of the process tries to change files in wordpress directory. But, the owner, _nginx_, does not have a permission to change the wordpress directory so the problem occurs.

**Solution**
Change the owner of wordpress directory to the owner of nginx (apache) service.

# chown -R [_owner]_:[_group of the owner]_ [_wordpress directory]
_Ex> chown -R nginx:nginx wordpress

You can check the owner of _nginx_ process by _ps -ef | grep nginx_ (or something like _ps -ef|grep httpd_ in the case of using apache).
