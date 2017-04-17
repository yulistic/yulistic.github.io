---
author: yulistic
comments: true
date: 2016-05-12 06:49:06+00:00
type: post
link: http://yulistic.com/?p=118
slug: mint-linux-samba-client-connection
title: '[Mint Linux] Samba client connection to Windows samba server'
wordpress_id: 118
language:
- English
tags:
- mint linux
- samba
- samba client
topics:
- Issues
---

Problem: I want to connect to samba server (windows machine) from linux machine.

Solution: use _smbclient_.

**1. Check the available samba folder in samba server machine.**

_smbclient -L //_[url of samba server or ip address]_/_

Find the _sharename_ that is used as samba share folder.

**2. Connect to the samba folder.**

_smbclient //_[url of samba server or ip address]_/_[shared folder]_ -U [_username_]_

If connected successfully, terminal shows as below.

-------------------------------
_Domain=[WORKGROUP] OS=[Unix] Server=[Samba 3.4.7]_
_smb: >_
------------------------------

**3. If you want to mount remote samba folder to local directory, use following command.**

_sudo mount -t cifs //_[url of samba server or ip address]_/_[shared folder] [local directory path]_ -o username=_[username]_,password=_[password]

**4. You can make samba folder mounted automatically when system starts, by adding following line to _/etc/fstab _.**

_//_[url of samba server or ip address]_/_[shared folder]  [local directory path] _cifs username=_[username]_,password=_[password]_,iocharset=utf8   __0   0_

(_iocharset=utf8_ is an option.)








