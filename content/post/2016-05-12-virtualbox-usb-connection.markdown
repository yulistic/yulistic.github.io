---
author: yulistic
comments: true
date: 2016-05-12 06:49:06+00:00
layout: post
link: http://yulistic.com/?p=126
slug: virtualbox-usb-connection
title: Virtualbox USB connection
wordpress_id: 126
language:
- English
topics:
- Issues
---

Problem: Virtualbox does not recognize host's USBs. Being different from the below screenshot, none of USBs was recognized.

Environment: Mint Linux 17, Virtualbox 4.3.10, Virtualbox Guest Additions 4.3.10 (not 4.3.14)

[caption id="attachment_128" align="aligncenter" width="854"][![Selection_017](http://yulistic.com/wp-content/uploads/2014/08/Selection_017.png)](http://yulistic.com/wp-content/uploads/2014/08/Selection_017.png) After the problem had been fixed, the list of connected USBs were displayed. There was no USB detected before the problem had been solved.[/caption]

Solution: Add current user to the _vboxusers_.

Ex> _$ adduser _[user name]_ vboxusers_

After reboot the system, USBs are detected.
