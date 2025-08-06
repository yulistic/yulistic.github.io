---
author: yulistic
comments: true
date: 2016-05-12 06:49:06+00:00
type: post
link: http://yulistic.com/?p=160
slug: linux-mint-17-install-nvidia-driver
title: '[Linux Mint 17] Install NVIDIA driver'
wordpress_id: 160
language:
- English
topics:
- Linux
- Issues
---

Refer to the following link.
My installation succeeded with second method in the site:"**FOR BINARY DRIVERS**" [link](http://ubuntuforums.org/showthread.php?t=2081649)

----- Appended, 2015-10-15



	
  1. Blacklist _nouveau_. Refer to [link](http://askubuntu.com/a/481540).

	
  2. Download the proper Nvidia driver corresponding to your GPU.

	
  3. Install the driver.
1) Press _[Ctrl]+[Alt]+[F1]_ and go to the terminal mode.
2) `sudo service mdm stop` (in the case of mint linux).
3) Install Nvidia driver (sudo sh NVIDIA~~~).

	
  4. Reboot.


