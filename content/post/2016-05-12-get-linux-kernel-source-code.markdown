---
author: yulistic
comments: true
date: 2016-05-12 06:49:07+00:00
layout: post
link: http://yulistic.com/?p=412
slug: get-linux-kernel-source-code
title: Get Linux Kernel source code
wordpress_id: 412
language:
- English
tags:
- kernel source code
- linux kernel
topics:
- Linux
- Tips
---

To get the source code of current Linux kernel,

    
    $ sudo apt-get source linux-image-$(uname -r)


Reference: [Ubuntu wiki: BuildYourOwnKernel](https://wiki.ubuntu.com/Kernel/BuildYourOwnKernel)
