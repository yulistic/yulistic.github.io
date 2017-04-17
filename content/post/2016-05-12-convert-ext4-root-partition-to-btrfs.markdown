---
author: yulistic
comments: true
date: 2016-05-12 06:49:07+00:00
type: post
link: http://yulistic.com/?p=356
slug: convert-ext4-root-partition-to-btrfs
title: Convert ext4 root(/) partition to btrfs
wordpress_id: 356
language:
- English
tags:
- btrfs
- convert to btrfs
- copy-on-write
- copy-on-write file system
topics:
- Linux
- Issues
- Tips
---

# Purpose


Let's make a root(`/`) partition except `/boot` directory be `btrfs`. `btrfs` supports a copy-on-write functionality.

For the reason of excepting `/boot` partition, the Ubuntu document warns against including _Grub_ into `btrfs` partition.


<blockquote>... As of 11.04, it is possible to use only btrfs file systems with the caveat that grub 'MUST NOT' be installed to the boot sector of the btrfs volume containing /boot. (from [link](https://help.ubuntu.com/community/btrfs))</blockquote>


As a result, I decided to make the `/boot` partition be separated from the root(`/`) partition.


# Prerequisites





	
  * Live bootable USB or Live CD of Ubuntu (refer to link: [Making Live bootable USB](http://yulistic.com/problems-solutions/361))

	
  * Make boot partition be separated from your btrfs partition. (refer to link: [Create boot partition after installation](http://yulistic.com/problems-solutions/330))

	
  * Grub Legacy (not Grub2. Refer to link: [Downgrade Grub2 to Grub Legacy](http://yulistic.com/en/linux-2/399))




# Reference


Basically, refer to the [link](http://ubuntuforums.org/showthread.php?t=1389279) for a whole process. This article is just for supporting the referenced site.


# Problems & Solutions




## Booting with Live USB


During the process, you need to `umount` the directory to be converted to `btrfs`. In this article, we are converting the whole root partition, so it is required to be booted with Live USB. Otherwise, you will fail to command `btrfs-convert`, being prompted something like: `/dev/sda1 is mounted.`


## Cannot install `btrfs-tools` in Lively booted system


You might fail to install `btrfs-tools` because `apt-get` cannot find the package from repositories. Including all the repository will resolve this problem.



	
  1. Go to _Application > Ubuntu Software Center_

	
  2. From menu, _Edit > Software Sources_

	
  3. Check all the list in _Download from the Internet_

	
  4. Retry `apt-get install btrfs-tools`


**Updated**

It is recommended to use an updated version of `btrfs-tools`. You can get `[btrfs-tools_0.19+20100601-3ubuntu3_amd64.deb](http://ftp.acc.umu.se/ubuntu/pool/main/b/btrfs-tools/btrfs-tools_0.19+20100601-3ubuntu3_amd64.deb) `from [link](http://ftp.acc.umu.se/ubuntu/pool/main/b/btrfs-tools/) and install as below.

    
    sudo dpkg -i btrfs-tools_0.19+20100601-3ubuntu3_amd64.deb


Without this updated tool, you cannot delete `snapshot` of `btrfs`.


## Success of `btrfs-convert`


If you succeeded in `btrfs-convert`, the following messages will be prompted.

    
    ubuntu@ubuntu:~$ sudo btrfs-convert /dev/sda1
    creating btrfs metadata.
    creating ext2fs image file.
    cleaning up system chunk.
    conversion complete.
    




## Change UUID in `menu.lst` file


With _Grub Legacy_ we need to modify `root=UUID` value in `menu.lst` file to `btrfs` partition's manually. I used the following lines for _Grub_'s `menu.lst` file.

    
    title       Linux 2.6.32.67
    uuid        89591593-766e-4565-9d5c-017fb0e33298
    kernel      /vmlinuz-2.6.32.67 root=UUID=a90c79b1-5883-44cc-9e74-752db9ca764d ro
    initrd      /initrd.img-2.6.32.67


In this example, **`a90c79b1-5883-44cc-9e74-752db9ca764d`** is the UUID of `btrfs` partition and **`89591593-766e-4565-9d5c-017fb0e33298`** is UUID of `/boot` partition.

Also, I used following lines for my `/etc/fstab` file.

    
    /dev/sda3       /boot       ext4     defaults       0       0   
    /dev/sda1       /           btrfs    defaults        0       1


As you can see, I just wrote a path (`/dev/sda1`) instead of UUID as described in the referenced site.


## Update `initrd` images


Because some scripts and hooking are added to `initramfs`, `initrd` images in `/boot` directory should be updated.

I could not update them with command (i.e. `update-initramfs -u -k all`) described in the referenced site. It was guessed due to the kernel version difference between Live USB and my original installation. I designated the kernel version as a parameter like below and it worked.

    
    update-initramfs -u -k 2.6.32.67


Good luck! :)
