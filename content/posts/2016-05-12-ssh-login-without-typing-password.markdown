---
author: yulistic
comments: true
date: 2016-05-12 06:49:07+00:00
type: post
link: http://yulistic.com/?p=429
slug: ssh-login-without-typing-password
title: ssh login without typing password
wordpress_id: 429
language:
- English
topics:
- Linux
- Tips
---

# Purpose


Let's do ssh login without being prompted to enter the password.



	
  1. From client, generate key with the following command.



    
    $ ssh-keygen


Type `enter`, without setting a passphrase.

2. From client, copy the generated key to the server.

    
    $ ssh-copy-id yulistic@123.456.789.123


3. Login to the server without entering your password.


# Tip.


You can copy public key to remote server manually.

In the local machine, by appending the key of local machine (content of file: _**~/.ssh/id_rsa.pub**_) to the file in the remote machine (**_~/.ssh/authorized_keys_**).

If the **_authorized_keys_** file does not exist in the remote machine, just generate a new one.
