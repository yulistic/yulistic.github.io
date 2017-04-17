---
author: yulistic
comments: true
date: 2016-05-12 06:49:07+00:00
type: post
link: http://yulistic.com/?p=330
slug: create-boot-partition-after-installation
title: Create boot partition after installation
wordpress_id: 330
language:
- English
tags:
- boot partition
- separate boot partition
topics:
- Linux
- Issues
---

# Problem


Make a boot partition be separated from the root partition without re-installation.


# Environment





	
  * Ubuntu 10.04.04

	
  * Live USB (Burned with _UNetbootin_)

	
  * Grub legacy




# Solution


Basically refer to [link](https://help.ubuntu.com/community/CreateBootPartitionAfterInstall). The site mentions two methods: _Easy way_ and _Manual way_. Firstly, I tried _Easy way_ but failed because of some problems in a tool, `boot-repair`. I recommend to follow _Manual way_ and the following explanations are also related to that way.



	
  1. Boot Ubuntu with the Live USB or Live CD.

	
  2. Make a new partition for `/boot` with _GParted_ tool. You can shrink existing partition to retain a space for the new boot partition. Please refer to the_ Step 3_ and _4_ of the _[Easy way](https://help.ubuntu.com/community/BootPartition)_.

	
  3. Just follow the instructions on the reference site. When mounting drives (boot and main) you might fail because of no sufficient space in root(`/`) partition for mounting. I instead used `/tmp` directory for mounting. (`/tmp/boot` for the new boot partition and `/tmp/main` for the previous root(`/`) partition)

	
  4. `umount` also failed because of the lack of space. `-n` option will help you to `umount` without saving data to `/etc/mtab`.

    
    error writing /etc/mtab.tmp: No space left on device




	
  5. When you setting up GRUB Legacy, the site shows an example for `(hd0,1)`. It is because the example is dealing with `/dev/sda2` as its new boot partition. In my case, a new boot partition was `/dev/sda3` in which case root should be `(hd0,2)`.
Alternatively, you can set the _menu.lst_ file as below writing UUID directly.

    
    title       Linux 2.6.32.67
    uuid        89591593-766e-4565-9d5c-017fb0e33298   # UUID of your boot partition.
    kernel      /vmlinuz-2.6.32.67 root=UUID=fa565f6c-76a9-4c2a-ac8b-2003f97ed7be ro   # UUID of your root(/) partition
    initrd      /initrd.img-2.6.32.67




	
  6. When re-installing grub, you should input proper values corresponding to your machine state. For example, my boot partition was `/dev/sda3`, so I needed to write `root (hd0,2)` and `setup (hd0)`.
(`hd0` means `sda`, `2` in `(hd0,2)` means `3` in `sda3`)


