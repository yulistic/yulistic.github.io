+++
author = "yulistic"
date = "2017-12-06T11:57:53+09:00"
description = "Access to reserved memory in Linux"
draft = false
tags = ["linux","kernel"]
title = "Access to reserved memory in Linux kernel"
topics = ["linux"]
type = "post"

+++

I would like to write a kernel module that uses some memory space for its own purpose.


# Reserve memory space with kernel parameter

The memory space was reserved through linux kernel parameter by modifying `/etc/default/grub` as below.  
`sudo update-grub` and rebooting should follow to apply the modification.  
The reserved area was from `0x100000000` ~ `0x1ffffffff` (4GB~8GB).

```
GRUB_CMDLINE_LINUX_DEFAULT="memmap=4G\\\$0x100000000"
```
After rebooting, you can confirm the reduced memory space with the command `cat /proc/meminfo`.


# Access to the reserved memory area 
I could access to the reserved memory space in my kernel module with `ioremap_nocache()` function of linux kernel.  
Please refer to the source code([hello.c](https://gitlab.com/yulistic/code-snippets-linux-kernel/blob/master/reserved_memory/hello.c)) in the [repo](https://gitlab.com/yulistic/code-snippets-linux-kernel/tree/master/reserved_memory).
