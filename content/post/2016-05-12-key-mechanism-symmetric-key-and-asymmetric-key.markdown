---
author: yulistic
comments: true
date: 2016-05-12 06:49:06+00:00
layout: post
link: http://yulistic.com/?p=79
slug: key-mechanism-symmetric-key-and-asymmetric-key
title: 'Key mechanism: symmetric key and asymmetric key'
wordpress_id: 79
language:
- English
topics:
- Security
---

There are two key mechanisms: symmetric and asymmetric key mechanisms.

A symmetric key mechanism is not used recently because of difficulty of managing key. The key which is shared between two (or several) parties should be kept as secret.

An asymmetric key mechanism is also known as public-private key.  A private key is kept as secret by the key owner whereas a public key is known to anyone. Two use cases are considered for this mechanism.

The first case is to sign data. In this use case, data is transmitted from the key owner to other parties. The key owner signs data with private key and transmit it to other parties. The other party who received the data can check whether the data is from the real key owner with key owner's public key.





[caption id="attachment_81" align="aligncenter" width="300"][![The first use case (signing)](http://yulistic.com/wp-content/uploads/2014/01/Picture2-300x230.png)](http://yulistic.com/wp-content/uploads/2014/01/Picture2.png) The first use case (signing)[/caption]

The second case is to encrypt data. In this use case, data is transmitted from the one of other party to the key owner. The data is encrypted with key owner's public key by the other party and transmitted to the key owner. The only key owner can decrypt the data because she is the only one who possesses her private key. No other party can see the content of the data.

[caption id="attachment_82" align="aligncenter" width="300"][![The second use case](http://yulistic.com/wp-content/uploads/2014/01/Picture3-300x170.png)](http://yulistic.com/wp-content/uploads/2014/01/Picture3.png) The second use case[/caption]

*RSA is an algorithm for the asymmetric key mechanism.
