---
author: yulistic
comments: true
date: 2016-05-12 06:49:06+00:00
layout: post
link: http://yulistic.com/?p=88
slug: install-wordpress-with-mysql-php-and-nginx
title: Install Wordpress with MySQL, PHP and Nginx.
wordpress_id: 88
language:
- English
topics:
- Problems &amp; Solutions
---

Problem: To install _wordpress_ based on the _mysql_ database system and _nginx_ web server.



**1. Install MySQL.**

1-1. If there exists any package installed already, erase it.

1-2. Download all the mysql packages from the site.

1-3. Install all the downloaded packages through the following order.



	
  * MySQL-client

	
  * MySQL-devel

	
  * MySQL-embedded

	
  * MySQL-server

	
  * MySQL-shared

	
  * MySQL-shared-compat

	
  * MySQL-test




**2. Install Nginx
**

2-1. Add repository

Add a new file "nginx.repo" to the "_/etc/yum.repos.d/_" with the following contents.

========================= nginx.repo ===
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/mainline/centos/$releasever/$basearch/
gpgcheck=0
enabled=1
======================================

2-2. Install through yum.

_> yum install nginx_



**3. Install PHP-FPM**

Nginx executes PHP through FPM.

_> yum install php
> yum install php-fpm_

Change _"__/etc/nginx/conf.d/default.conf"_ file.

============================= default.con f===
...

server_name   **yulistic.com**;

...

location / {

root   **/usr/share/nginx/html/wordpress**;

index  **index.php** index.html index.htm;

}

...

location ~ .php$ {

root           **/usr/share/nginx/html/wordpress**;

fastcgi_pass   127.0.0.1:9000;

fastcgi_index  **index.php**;

#fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;

fastcgi_param  SCRIPT_FILENAME  **$document_root**$fastcgi_script_name;

include        fastcgi_params;

    }

...
==========================================



**4. Install Wordpress**

Download wordpress tar file from the wordpress website and unzip it.

Move the wordpress directory to the web home directory (default directory is: /usr/share/nginx/html).

You can progress installation by accessing the page through web browser (ex> yulistic.com or ip address).
