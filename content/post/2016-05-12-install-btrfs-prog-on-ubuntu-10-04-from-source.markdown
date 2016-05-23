---
author: yulistic
comments: true
date: 2016-05-12 06:49:07+00:00
layout: post
link: http://yulistic.com/?p=401
slug: install-btrfs-prog-on-ubuntu-10-04-from-source
title: Install btrfs-prog on Ubuntu 10.04 from source
wordpress_id: 401
language:
- English
tags:
- btrfs-prog
- zlib
topics:
- Linux
- Problems &amp; Solutions
---

# 1. Purpose


To install btrfs-prog on Ubuntu 10.04 from the source.


# 2. Reference


btrfs wiki page: [wiki](https://btrfs.wiki.kernel.org/index.php/Btrfs_source_repositories)


# 3. Problems




## 3.1. Install _autogen_ for `./autogen.sh`



    
    sudo apt-get install autoconf




## _3.2. E_rrors during `./configure`


Error message of _"No package found"_ errors are like below.

    
    ...
    checking for mv... /bin/mv
    checking for a sed that does not truncate output... /bin/sed
    checking for EXT2FS... configure: error: Package requirements (ext2fs) were not met:
    
    No package 'ext2fs' found
    
    Consider adjusting the PKG_CONFIG_PATH environment variable if you
    installed software in a non-standard prefix.
    
    Alternatively, you may set the environment variables EXT2FS_CFLAGS
    and EXT2FS_LIBS to avoid the need to call pkg-config.
    See the pkg-config man page for more details.





	
  * 


### No package _'ext2fs'_ found





Install _'e2fslibs-dev'_.

    
    $ sudo apt-get install e2fslibs-dev





	
  * 


### No package _'blkid'_ found





Install _'libblkid-dev'_.

    
    $ sudo apt-get install libblkid-dev





	
  * 


### No package 'zlib' found.





Download _zlib_ package from [here](https://launchpad.net/ubuntu/+source/zlib/1:1.2.3.3.dfsg-15ubuntu1). I used file: _zlib_1.2.3.3.dfsg.orig.tar.gz_. Please check your Ubuntu version.

Decompress the downloaded _zlib_ package file and install it as below.

    
    $ ./configure
    $ make test
    $ sudo make install





	
  * 


### Cannot find _lzo2_ library





Install _'liblzo2-dev'_.

    
    $ sudo apt-get install liblzo2-dev


Finally, installation succeeded.


