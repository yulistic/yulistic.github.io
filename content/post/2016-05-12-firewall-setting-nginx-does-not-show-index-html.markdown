---
author: yulistic
comments: true
date: 2016-05-12 06:49:06+00:00
layout: post
link: http://yulistic.com/?p=84
slug: firewall-setting-nginx-does-not-show-index-html
title: Firewall setting (Nginx does not show index.html)
wordpress_id: 84
language:
- English
topics:
- Issues
---

**Environment**: CentOS 6.5, nginx 1.5.9

**Problem**: _Nginx_ is installed through _yum_ but does not show _index.html_(the first page) in the web browser.

**Reason of the problem**: The problem was the firewall. You can check it from /etc/sysconfig/iptables. Refer to the following solution.

**Solution**:



	
  1. Open  _/etc/sysconfig/iptables_.

	
  2. Append _-A INPUT -m state --state NEW -m tcp -p tcp --dport 80 -j ACCEPT_

	
  3. _sudo service iptables restart_





