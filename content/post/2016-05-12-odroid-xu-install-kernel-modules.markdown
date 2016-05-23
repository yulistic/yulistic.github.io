---
author: yulistic
comments: true
date: 2016-05-12 06:49:06+00:00
layout: post
link: http://yulistic.com/?p=163
slug: odroid-xu-install-kernel-modules
title: '[ODROID-XU] install kernel modules'
wordpress_id: 163
language:
- English
topics:
- Problems &amp; Solutions
---

When you rebuild your own kernel and upload it on your ODROID-XU board with Android system, the kernel modules should be uploaded too.

If not, the following message will be prompted in booting time.

_smsc95xx: version magic '3.4.5 SMP preempt mod_unload ARMv7 p2v8 ' should be '3.4.5-00019-gc81eeaf-dirty SMP preempt mod_unload ARMv7 p2v8 '_

---------------------

[Problem]

The situation is that your kernel (including kernel modules) has been compiled and uploaded to your ODROID-XU successfully. But, the error message is prompted in booting time (like above) and network cannot be configured displaying message like:
_init: no such service 'dhcpcd_'_

[Solution]

First, check which modules need to be replaced.

You can check the list of modules in ODROID-XU (Android)'s directory:_ /system/lib/modules/_

In my case, the system has two modules:

_shell@android:/ $ ls /system/lib/modules_
_ rtl8192cu.ko_
_ smsc95xx.ko_

Second, in your host PC, find the modules newly compiled. (_rtl8192cu.ko_ is the name of the kernel module)

_find . -name "rtl8192cu.ko"_
_ ./drivers/net/wireless/rtl8192cu_v40/rtl8192cu.ko_

Third, _adb remount_ if not, you cannot change the kernel module file because it is read-only file system.

Last, push the module to the same position where the prior one exists. (using _adb push_)

_adb push ./drivers/net/wireless/rtl8192cu_v40/rtl8192cu.ko /system/lib/modules/_

You need to replace all the kernel modules in the same way. After doing that, _adb reboot_ and enjoy your ODROID.
