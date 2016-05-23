---
author: yulistic
comments: true
date: 2016-05-12 06:49:06+00:00
layout: post
link: http://yulistic.com/?p=138
slug: remove-partition-and-format-sdcard-in-mint-linux
title: Remove partition and format SD Card in Mint Linux
wordpress_id: 138
language:
- English
tags:
- mint linux
- SD card format
- SD card partition
topics:
- Problems &amp; Solutions
---

1. Find the name of the SD card. (ex> **_/dev/sdd_ in my case. You must enter your own SD card device name.**)
# sudo fdisk -l

If SD card is already mounted, unmount it.
# sudo umount **_[/dev/sdd]_**



2. Remove partition.

# sudo fdisk _**[/dev/sdd]**_

You can delete partition by entering d. (Refer to following info.)

m: help.
d: delete partition.
p: print current partition information.
n: make new partition.
w: save and exit.



3. Format SD card.

# sudo mkfs.ext2 **_[/dev/sdd]_**



4. Mount your SD card.

# sudo mount _**[/dev/sdd]**_ [mount directory]
