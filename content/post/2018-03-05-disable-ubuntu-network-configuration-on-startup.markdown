+++
author = "yulistic"
date = "2018-03-05T20:40:48+09:00"
description = "Disable Ubuntu's network configuration checking on its startup (on boot)"
draft = false
tags = ["boot","startup", "Ubuntu", "network"]
title = "Disable Ubuntu network configuration on startup (on boot)"
topics = ["tips", "issues"]
type = "post"

+++

# Intro.
Ubuntu checks network configuration on its startup.
Although this process passes quickly when the network connection is normal, it takes about __5 minutes__ if there exist some problems in the configuration.  
There is a way to reduce the waiting time for the network configuration.

# Reference
[Ubundtu forum answer](https://ubuntuforums.org/showthread.php?t=2323253&p=13489687#post13489687)

# Solution
You can change the value of the waiting time.
Set the value of `TimeoutStartSec` in the file, `/lib/systemd/system/networking.service`.  
For example,
```
...
TimeoutStartSec=15sec
...
```
My system was Ubuntu 16.04, FYI.

_Good luck! :D_
