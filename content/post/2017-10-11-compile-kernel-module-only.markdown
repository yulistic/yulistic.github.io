+++
author = "yulistic"
date = "2017-10-11T14:43:18+09:00"
description = "Compiling a kernel module only without a whole kernel compilation."
draft = false
tags = ["linux","kernel", "kernel compiling", "kernel module"]
title = "Compiling kernel module only w/o whole kernel compilation"
topics = ["linux"]
type = "post"

+++

# Intro.
I was tried to modify a `kvm` kernel module for my research.
Because it was a built-in kernel module, I needed to build all the kernel source code after modifying `kvm` module which is located in path `arch/x86/kvm/` from the linux kernel source root.  
The whole kernel compilation was a time consuming job, usually taking over 10 minutes even on my i7 desktop machine.
I tried to find a way to compile modules only without the whole kernel compilation.
The solution and some troublesomes are described below.

# Assumptions
It is assumed that you have a kernel source code and configured it properly according to your taste. Also, assumed that you had installed the kernel and rebooted with it.

# Solution
Building only one module is easy. After configuring, build the source as following.

```lang=shell
make M=path/to/module/directory
make M=path/to/module/directory modules_install
```
You can find the path of modules with `modinfo` command.  
In my case, the required module was `kvm.ko`, and `kvm-intel.ko`. They were located in `arch/x86/kvm`.

```lang=shell
make M=arch/x86/kvm
make M=arch/x86/kvm modules_install
```

You can reload the new modules.
I removed the `kvm-intel` module first because it depends on the `kvm` module.
```lang=shell
sudo rmmod kvm-intel kvm
```
And, load the new modules.
```lang=shell
sudo modprobe kvm
sudo modprobe kvm-intel
```
or just loading `kvm-intel` will load `kvm` automatically.
```lang=shell
sudo modprobe kvm-intel
```

FYI, the new modules are installed in ``/lib/modules/`uname -r`/extra`` directory.


# Troublesomes

## 1. `modprobe` failure.
```lang=shell
modprobe: error: could not insert 'kvm': exec format error
```
The modprobe might fail if the version of a kernel module and that of a kernel are different.
You can check the error with `dmesg` after the `modprobe` failure.  
In my case, I built the kernel without any modification which resulted in the version number of `4.13.0-rc6`.
When I modified the `kvm` module and compiled it, the version number was changed to `4.13.0-rc6+`. Linux kernel source code appends `+` to the version number as LOCALVERSION if any source code is modified. (It might be related to `git`'s uncommitted or unstaged changes. I did not confirmed yet.)

My solution was building the kernel with some small modifications generating the version number as `4.13.0-rc6+` as a baseline.  
The problem solved because the kvm module was also built with the same version number, `4.13.0-rc6+`, which did not produce any `modprobe` error.

## 2. Location of generated modules
The modules generated with `M=path` options are installed into ``/lib/modules/`uname -r`/extra`` path.
The path is different from the originally built one (when compiling the whole kernel) which is ``/lib/modules/`uname -r`/kernel/arch/x86/kvm`` in the case of `kvm`.

If you want to install a new module into the same location of original one, use `INSTALL_MOD_DIR` option. Example follows.

```lang=shell
sudo make INSTALL_MOD_DIR=kernel/arch/x86/kvm M=arch/x86/kvm modules_install
```
Note that you have to do `sudo depmod -a` before `modprobe` the new modules. Otherwise, `modprobe` will fail.
