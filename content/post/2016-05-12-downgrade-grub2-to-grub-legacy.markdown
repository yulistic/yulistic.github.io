---
author: yulistic
comments: true
date: 2016-05-12 06:49:07+00:00
layout: post
link: http://yulistic.com/?p=399
slug: downgrade-grub2-to-grub-legacy
title: Downgrade Grub2 to Grub Legacy
wordpress_id: 399
language:
- English
tags:
- grub
- grub downgrade
- grub legacy
topics:
- Linux
---

## 1. Backup for Grub2 settings



    
    $ sudo cp /etc/default/grub /etc/default/grub.old
    $ sudo cp -R /etc/grub.d /etc/grub.d.old
    $ sudo cp -R /boot/grub /boot/grub.old




## 2. Remove Grub2



    
    $ sudo apt-get purge grub2 grub-pc




## 3. Install Grub Legacy



    
    $ sudo apt-get install grub




## 4. Update Grub settings



    
    $ sudo update-grub
    $ sudo grub-install /dev/sdX


*sdX should be matched your machine state. Usually, it is `/dev/sda`.


## 5. Block the update of Grub Legacy



    
    $ echo “grub hold” | sudo dpkg --set-selections





