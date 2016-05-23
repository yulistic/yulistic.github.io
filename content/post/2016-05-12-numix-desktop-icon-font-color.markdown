---
author: yulistic
comments: true
date: 2016-05-12 06:49:07+00:00
layout: post
link: http://yulistic.com/?p=276
slug: numix-desktop-icon-font-color
title: Numix theme desktop icon font color
wordpress_id: 276
language:
- English
topics:
- Linux
- Problems &amp; Solutions
---

# Problem


With Numix theme, desktop icon font color is dark. It is hard to read icon label when I changed my desktop background (wallpaper) to a dark one.


# Solution


Refer to the [link](http://forums.linuxmint.com/viewtopic.php?f=42&t=118989#p868071).

Briefly speaking, change the file, "`/usr/share/themes/Numix/gtk-3.0/apps/gnome-applications.css`", as below.

Replace "`nautilus`" with "`nemo`".
