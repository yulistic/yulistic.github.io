---
author: yulistic
title: "Reducing initrd size"
description: "How to reduce initrd file size on Ubuntu."
date: 2020-11-20T16:42:09+09:00
tags: ["linux"]
topics: ["issues"]
type: "post"
draft: false
---

# Problem
`/boot` partition is too small to include a new initrd file. A Linux kernel installation from soruce code fails as below.
```
make -j`nproc`
sudo make modules_install
sudo make install <-- it fails.
```
Error messages are like below.
```
$ sudo make install
sh ./arch/x86/boot/install.sh 5.3.11 arch/x86/boot/bzImage \
        System.map "/boot"
run-parts: executing /etc/kernel/postinst.d/apt-auto-removal 5.3.11 /boot/vmlinuz-5.3.11
run-parts: executing /etc/kernel/postinst.d/initramfs-tools 5.3.11 /boot/vmlinuz-5.3.11
update-initramfs: Generating /boot/initrd.img-5.3.11
W: Possible missing firmware /lib/firmware/ast_dp501_fw.bin for module ast

gzip: stdout: No space left on device
E: mkinitramfs failure cpio 141 gzip 1
update-initramfs: failed for /boot/initrd.img-5.3.11 with 1.
run-parts: /etc/kernel/postinst.d/initramfs-tools exited with return code 1
arch/x86/boot/Makefile:155: recipe for target 'install' failed
make[1]: *** [install] Error 1
arch/x86/Makefile:293: recipe for target 'install' failed
make: *** [install] Error 2
```

# Solution
In Ubuntu 18.04, when kernel installation (`make install`) is failed.
```
cd /lib/modules/<kernel_version>
sudo find . -name "*.ko" -exec strip --strip-unneeded {} +
cd /<path>/<to>/<linux-kernel_src>
sudo make install
```

# Reference
* https://unix.stackexchange.com/a/270394
