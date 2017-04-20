---
author: yulistic
comments: true
date: 2016-05-12 06:49:07+00:00
type: post
link: http://yulistic.com/?p=284
slug: linux-login-ssh-without-password-input
title: '[Linux] Login SSH without password input'
wordpress_id: 284
language:
- English
topics:
- Linux
---

# Problem

I want to access remote machine without typing password.

# Term.

Remote machine: target machine to which I want to access through `ssh`.  
Local machine: local machine from which I try to access to the remote machine.


# Solution

In a word, We can do it by using **public-private key**.
	
  * Private key should be in local machine and it must not be exposed (keep it secret).
  * Public key will be in remote machine not to prompt password in every ssh access.
	
**1. Key generation in local machine** (If you already have one, you don't need to regenerate key. Check `~/.ssh/id_rsa.pub`.)  
Use `ssh-keygen`.

```bash
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/yulistic/.ssh/id_rsa): 
Created directory '/home/yulistic/.ssh'.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/yulistic/.ssh/id_rsa.
Your public key has been saved in /home/yulistic/.ssh/id_rsa.pub.
The key fingerprint is:
7a:5a:8e:14:3b:5d:10:03:14:39:01:18:5c:5a:50:b7 yulistic@hostname
The key's randomart image is:
+--[ RSA 2048]----+
| .o*=o*=o        |
|  oo .o. o       |
|  .   E..        |
|         .       |
|      . S .      |
|       = .       |
|      = +        |
|     . B         |
|      o .        |
+-----------------+ 
```
	
**2. Copy the generated public key to remote machine.** 
    
```bash
$ ssh-copy-id yulistic@remote.server.com
The authenticity of host 'remote.server.com (123.456.789.111)' can't be established.
RSA key fingerprint is b0:6c:87:0b:2f:ae:5c:09:21:d6:0a:d5:01:fe:28:db.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'remote.server.com,123.456.789.111' (RSA) to the list of known hosts.
yulistic@remote.server.com's password: 
Now try logging into the machine, with "ssh 'yulistic@123.456.789.111'", and check in:

  .ssh/authorized_keys

to make sure we haven't added extra keys that you weren't expecting.
```
	
**3. Access to the remote machine through `ssh`. If it does not prompt to input password, then it is successful.**  
	
**4. If it still ask password, check your `~/.ssh` directory permission at the remote machine. Refer to [link](http://www.openssh.org/faq.html#3.14).**  
	
**5. It might have another problem if you are using SELinux.**

# Reference
* [link (Korean)](http://lesstif.com/pages/viewpage.action?pageId=12943452)
