---
title: "Debugging linux kernel with GDB and Qemu"
date: 2018-12-03T20:40:14+09:00
description: "Debugging Linux kernel line by line using GDB and Qemu."
tags: ["Linux","debug", "gdb", "qemu", "kernel"]
topics: ["linux"]
type: "post"
---

# Intro.
In this page I'll briefly introduce how to setup the environment for debugging a linux kernel with GDB and Qemu. The linux kernel runs on Qemu being virtualized.

# Process
1. Build the linux kernel that you want to debug.
 * Check the configuration. Set `CONFIG_DEBUG_INFO=y` if not configured.
 * You can build the kernel as deb or rpm to install on remote servers. Use commands: `make bindep-pkg -j4`, `make rpm-pkg -j4`. (In the case of deb, package `alien` is required. Install it with `apt`.)
2. Install qemu. Refer to the [official site](https://www.qemu.org/download/#source).
 * Configure example: `./configure --target-list=x86_64-softmmu --enable-debug`
3. Install VM. (In this example, I installed ubuntu 16.04.)
 * Download ubuntu iso file.
 * Create qemu img named as 'test.qcow2': `./qemu-img create -f qcow2 test.qcow2 16G`
 * Boot VM with ubuntu iso image: `x86_64-softmmu/qemu-system-x86_64 -m 2048 -enable-kvm -drive if=virtio,file=test.qcow2,cache=none -cdrom ubuntu-16.04.5.iso`
  * You can use `-vnc :1` option when accessing remotly through ssh.
 * After installation, start VM without the `--cdrom ~~.iso` option.
4. Replace the default kernel of VM with the version you built.
 * Copy deb files to the VM and `sudo dpkg -i *.deb`.
5. Add kernel parameter `nokaslr`. It is required to make breakpoint work correctly.
 * Append `nokaslr` to the `GRUB_CMDLINE_LINUX_DEFAULT` in `/etc/default/grub`.
 * Execute `update-grub`
 *  Restart the VM.
5. Make symbol file from `vmlinux` kernel image. `vmlinux` file is located in the kernel source directory (generated after compilation).
```
objcopy --only-keep-debug vmlinux kernel.sym
```
6. Run the qemu with the following options. `-S` stops qemu waiting gdb  and `-s` makes gdb be able to attach through `localhost:1234`.
```
# Example for qemu execution.
./x86_64-softmmu/qemu-system-x86_64 -s -S \
    -m 2048 \
    -chardev stdio,id=gdb0 \
    -drive if=virtio,file=nfstest.qcow2,cache=none \
    -device isa-debugcon,iobase=0x402,chardev=gdb0,id=d1 \
    -vga virtio \
    -enable-kvm \
    -vnc :1
```
The qemu stops waiting for the debugger to be attached.

6. Run `gdb`, load symbol file, and attach to the qemu execution.
```
gdb
(gdb) file ./kernel.sym
(gdb) target remote :1234
(gdb) hbreak start_kernel
(gdb) c
```
After type `c`, qemu continues to run and break at the `start_kernel` breakpoint.

# Other issues
* `gdb` does not find the source directory.
 * Use `dir /src/dir/path` command. (Not tested.)
* Change optimization options of a kernel compilation to eliminate any confusion while tracking the code with gdb.
 * Set `-Og` options for the files. As below example.
```
# Added to mm/Makefile for debugging.
CFLAGS_ksm.o = -Og
CFLAGS_huge_memory.o = -Og
CFLAGS_memory.o = -Og
CFLAGS_migrate.o = -Og
CFLAGS_page_alloc.o = -Og
```

# References
* https://wiki.osdev.org/Kernel_Debugging
* https://gist.github.com/hngouveia01/843a2202628c7d567dad0f657f8373aa
