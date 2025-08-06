---
author: yulistic
comments: true
date: 2016-05-12 06:49:07+00:00
type: post
link: http://yulistic.com/?p=361
slug: live-bootable-usb-for-ubuntu-10-04-04
title: Live Bootable USB for Ubuntu 10.04.04
wordpress_id: 361
language:
- English
topics:
- Linux
- Issues
- Tips
---

# Problem


I made a Live bootable USB of Ubuntu 10.04.04 with _Startup Disk Creator_ which was basically installed on my Mint 17 (distro. based on Ubuntu 14.04) machine.

But, booting was failed. It was waiting permanently on startup screen.

[caption id="" align="aligncenter" width="1024"]![](http://1.bp.blogspot.com/_4B7ZWQHqMpk/TMcEEwqP88I/AAAAAAAAAEc/uVUzQyc32Ik/s1600/boot1.png) Waiting permanently on startup screen[/caption]


# Solution


I used another program _UNetbootin_ which successfully booted Ubuntu 10.04.04. You can find the tool [here](https://unetbootin.github.io/).


# Tip


To make a live USB that can maintain some changes, set "_Space used to preserve files across reboots (Ubuntu only)_" as a positive value.

[caption id="attachment_372" align="aligncenter" width="526"][![](http://yulistic.com/wp-content/uploads/2015/11/UNetbootin_269.png)](http://yulistic.com/wp-content/uploads/2015/11/UNetbootin_269.png) UNetbootin window[/caption]
