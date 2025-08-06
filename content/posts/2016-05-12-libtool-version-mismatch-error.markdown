---
author: yulistic
comments: true
date: 2016-05-12 06:49:07+00:00
type: post
link: http://yulistic.com/?p=199
slug: libtool-version-mismatch-error
title: libtool version mismatch error
wordpress_id: 199
language:
- English
topics:
- Issues
---

# Problem


libtool version mismatch error


# Log message



    
    libtool: Version mismatch error. This is libtool 2.4.4, but the
    libtool: definition of this LT_INIT comes from libtool 2.4.2.
    libtool: You should recreate aclocal.m4 with macros from libtool 2.4.4
    libtool: and run autoconf again.




#  Solution



    
    autoreconf --force --install
    ./configure
    make



