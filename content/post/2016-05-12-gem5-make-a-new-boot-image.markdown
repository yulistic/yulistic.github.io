---
author: yulistic
comments: true
date: 2016-05-12 06:49:07+00:00
type: post
link: http://yulistic.com/?p=230
slug: gem5-make-a-new-boot-image
title: '[Gem5] Make a new boot image'
wordpress_id: 230
language:
- English
topics:
- Issues
- Tips
---

# Intro


I wanted to run a PARSEC 3.0 benchmark on Gem5 full system simulator. The original full system disk image provided by Gem5 official site could not be used as it is because the size of compiled PARSEC 3.0 benchmark was too large (about 10GB).

At first, I tried to mount a secondary disk image that contains benchmark files after Gem5's full system was booted. In this way, I can use the boot image (uploaded in the Gem5 official website) as it is and mount/unmount several other benchmark images as my wishes.

Unfortunately, I could not find the way opened in the internet. So, I chose the other way: make a new boot image including compiled benchmark files.


# Problem


Require larger boot image of Gem5 full system simluator so that it can contain the benchmark files.


# Background




## Gem5


It is assumed that you have already succeeded to boot a full system of Gem5 with following command in the Gem5 root directory.

    
    $ ./build/X86/gem5.opt configs/example/fs.py




## Commands


It is recommend to learn the role of following commands.

`dd`

`df`

`losetup`

`fdisk`

`mount`

`mke2fs`


# Solution




## 1. Make a new img file


Make a new image file with `dd` command. The output file will be filled with zeros. Here is an example.

    
    $ dd if=/dev/zero of=parsec3.img bs=1M count=12288


`if`: input file. In this example `zero`.

`of`: output file. In this example` parsec3.img.`

`count=12288` means total size of the output file will be 1MB * 12288 = 12GB

You can confirm that a new file has been successfully created with `ls -alh` command.

    
    $ ls -alh
    total 17G
    drwxrwxr-x  2 yulistic yulistic 4.0K  2월 22 20:00 .
    drwxrwxr-x 10 yulistic yulistic 4.0K  2월 22 18:38 ..
    ...
    -rw-rw-r--  1 yulistic yulistic  12G  2월 23 19:37 parsec3.img
    ...




## 2. Partitioning


After making a new image file being filled with zeroes, the file should have a partition. You can use any partition programs. `fdisk` is used here.

First, let's check the current status of image file.

    
    $ fdisk -l parsec3.img 
    
    Disk parsec3.img: 12.9 GB, 12884901888 bytes
    255 heads, 63 sectors/track, 1566 cylinders, total 25165824 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk identifier: 0x00000000
    
    Disk parsec3.img doesn't contain a valid partition table


It is saying that there is no partition in the image file.

With the following command, you can get into the partition program. You might require a root privilege.

    
    $ sudo fdisk parsec3.img


You can print help menu with option `m`. Option `n` will lead you to the process of making a new partition.

In this case, we don't need any secondary partition. Just make one partition as a whole with default values in the progress (just hit enter!).

After the process, save the modification and escape from the program with option `w`.

    
    $ sudo fdisk parsec3.img 
    [sudo] password for yulistic: 
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0x5fc418b5.
    Changes will remain in memory only, until you decide to write them.
    After that, of course, the previous content won't be recoverable.
    
    Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)
    
    Command (m for help): m
    Command action
     a toggle a bootable flag
     b edit bsd disklabel
     c toggle the dos compatibility flag
     d delete a partition
     l list known partition types
     m print this menu
     n add a new partition
     o create a new empty DOS partition table
     p print the partition table
     q quit without saving changes
     s create a new empty Sun disklabel
     t change a partition's system id
     u change display/entry units
     v verify the partition table
     w write table to disk and exit
     x extra functionality (experts only)
    
    Command (m for help): n
    Partition type:
     p primary (0 primary, 0 extended, 4 free)
     e extended
    Select (default p): p
    Partition number (1-4, default 1): 1
    First sector (2048-25165823, default 2048): 
    Using default value 2048
    Last sector, +sectors or +size{K,M,G} (2048-25165823, default 25165823): 
    Using default value 25165823
    
    Command (m for help): w
    The partition table has been altered!
    
    Syncing disks.


You can confirm that the partition has been created as below.

    
    $ fdisk -l parsec3.img 
    
    Disk parsec3.img: 12.9 GB, 12884901888 bytes
    128 heads, 33 sectors/track, 5957 cylinders, total 25165824 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk identifier: 0x5fc418b5
    
          Device Boot      Start         End      Blocks   Id  System
    parsec3.img1            2048    25165823    12581888   83  Linux




## 3. Formatting


Next, we need to format the partition. To make a virtual disk with image file, loop device will be used (losetup).

First, it is required to know the starting point of the partition. Again with the following command, you can figure out the start position of the partition.

    
    $ fdisk -l parsec3.img



    
    ...
          Device Boot      Start         End      Blocks   Id  System
    parsec3.img1            2048    25165823    12581888   83  Linux
    


We can check that the starting position of the partition is 2048.

Second, find an available loop device.

    
    $ sudo losetup -f
    /dev/loop0


Third, create virtual disk using loop device.

    
    $ sudo losetup -o $((512*2048)) /dev/loop0 parsec3.img


Fourth, use `mke2fs` command to format the partition as ext2.

    
    $ sudo mke2fs /dev/loop0


Last,  detach loop device.

    
    $ sudo losetup -d /dev/loop0




## 4. Copy benchmark files to image file


Mount your image file.

    
    $ mkdir tempdir
    $ sudo mount -o loop,offset=$((2048*512)) parsec3.img tempdir


or you can use loop device as Section 3.

    
    $ mkdir tempdir
    $ sudo losetup -o $((512*2048)) /dev/loop0 parsec3.img
    $ sudo mount /dev/loop0 tempdir


Copy your compiled benchmark files into the image file.

If you used loop device for mounting, you should detach loop device after use.

    
    $ sudo losetup -d /dev/loop0




## 5. Boot Gem5 full system simulator


Boot with your new image and run benchmark on Gem5 full system simulator.

    
    $ ./build/X86/gem5.opt configs/example/fs.py --disk-image=path/to/your/imagefile/parsec3.img
