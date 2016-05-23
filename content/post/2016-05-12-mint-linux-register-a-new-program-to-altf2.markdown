---
author: yulistic
comments: true
date: 2016-05-12 06:49:06+00:00
layout: post
link: http://yulistic.com/?p=112
slug: mint-linux-register-a-new-program-to-altf2
title: '[Mint Linux] Register a new program to Alt+f2'
wordpress_id: 112
language:
- English
topics:
- Problems &amp; Solutions
---

Environment: Mint Linux 17 64bit (on X86 machine)

Problem: I want to register a new program - locally built so it was not registered to the alt+f2 automatically - to alt+f2 command.

Solution: Symbolic link was used. (**-s** option is make link to be symbolic.)

$ sudo ln -s /your/program/execution/path /usr/bin/commandname

Example: I want to register mendeley program (paper management program) as alt+f2  command.

$ sudo ln -s /home/yulistic/programs/mendeley/bin/mendeleydesktop /usr/bin/mendeley

Then, I can start mendeleydesktop by **alt+F2** and "**mendeley**" keyword input.
