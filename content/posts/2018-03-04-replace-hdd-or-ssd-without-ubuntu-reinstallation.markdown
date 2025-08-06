+++
author = "yulistic"
date = "2018-03-04T15:14:55+09:00"
description = "Introduce a root partition migration to different storage (HDD or SSD) with Live USB."
tags = ["linux","Ubuntu","copy partition", "partition migration"]
title = "Replace HDD or SSD without the re-installation of Ubuntu"
topics = ["tips"]
type = "post"

+++

# Intro.
I tried to replace the HDD in my Ubuntu PC with a new SSD for the performance improvement.

# Reference
[1] [Partition copy and paste with GParted in the Ubuntu Live USB](https://askubuntu.com/questions/69283/how-to-upgrade-my-hdd-and-keep-my-ubuntu-11-10-instalation)  
[2] [Change UUID of a partition](https://askubuntu.com/questions/132079/how-do-i-change-uuid-of-a-disk-to-whatever-i-want)

# Solution

#### **_Please backup your data before starting the following processes._**
It is assumed that you have already installed a new storage HW into your PC. Also, Ubuntu live USB is required.

__1. Boot with the Ubuntu live USB.__  
<br>
__2. Start `gparted` which is a partition editor program.__  
<br>
__3. Select the original device in the top right corner.__  
[![Select original device](/img/2018-03-04/select_original_device.png "Select original device.")](/img/2018-03-04/select_original_device.png)

<br>
__4. Copy the partition that you want to migrate.__ If the original partition is larger than the new partition, shrink its size by *resizing* the partition.  
[![](/img/2018-03-04/copy_partition.png "Copy partition.")](/img/2018-03-04/copy_partition.png)

<br>
__5. Select the target device and paste the copied partition.__ If the device is in the first use, you need to create a new partition table before the paste. I chose `msdos` that was identical to original partition's. I checked it in the `/boot/grub/grub.cfg` file. Also, you can resize the pasted partition as you want.  
[![](/img/2018-03-04/paste_partition.png "Paste partition.")](/img/2018-03-04/paste_partition.png)

<br>
__6. If your original partition has a boot flag, which means it was a boot partition, you need to set the `boot` flag of the pasted partition.__  
[![](/img/2018-03-04/manage_flag.png "Manage flag.")](/img/2018-03-04/manage_flag.png)

[![](/img/2018-03-04/manage_flag_subwindow.png "Manage flag.")](/img/2018-03-04/manage_flag_subwindow.png)

<br>
__7. Apply all the changes.__  
[![](/img/2018-03-04/apply_changes.png "Apply changes.")](/img/2018-03-04/apply_changes.png)

<br>
__8. Re-install GRUB. If your partition is a boot partition.__ Check the new device name and the new partition name. For example, in my case, the new device(SSD) name was `/dev/sdc` and the partition name was `/dev/sdc1`. Run the following commands in a terminal.
```
sudo mount /dev/sdc1 /mnt
sudo grub-install --root-directory=/mnt /dev/sdc
sudo umount /mnt
```
<br>
__9. Change the `UUID` of the original partition with the following command.__ The `random` parameter will generate a new random `UUID` number.  
(This process is required because `gparted` copies all the data in a partition including `UUID`. You can find `UUID` of each partition with the `sudo blkid` command. The same `UUID` in two different partitions will confuse your operating system.)  
```
sudo tune2fs /dev/sdc1 -U random
```
<br>
__10. Reboot with the new partition. You might need to change the boot priority option in the BIOS.__
