---
author: yulistic
comments: true
date: 2016-05-12 06:49:06+00:00
type: post
link: http://yulistic.com/?p=92
slug: 404-not-found-permalink-error-wordpress-with-nginx
title: 404 not found permalink error (wordpress with nginx)
wordpress_id: 92
language:
- English
topics:
- Issues
---

**Problem**: I cannot see posts. It shows "404 not found".

**Solution**: Add "try_files $uri $uri/ /index.php;" to the _"location /"_ block in the nginx configuration file.

Refer to the following example.

========================== /etc/nginx/conf.d/default.conf =======
...
location / {
root /usr/share/nginx/html/yulistic;
index index.php index.html index.htm;
**try_files $uri $uri/ /index.php; **
}
...
===========================================================
