---
author: yulistic
comments: true
date: 2016-05-12 06:49:06+00:00
layout: post
link: http://yulistic.com/?p=171
slug: parsec-3-0-installation
title: PARSEC 3.0 installation issues
wordpress_id: 171
language:
- English
tags:
- installation
- parsec
- parsec 3.0
- simulator
topics:
- Issues
---

# 0. Refer to official site


([http://parsec.cs.princeton.edu/parsec3-doc.htm#simulation](http://parsec.cs.princeton.edu/parsec3-doc.htm#simulation))


# 1. Prerequisites: refer to requirements section in download page


([http://parsec.cs.princeton.edu/download.htm](http://parsec.cs.princeton.edu/download.htm))


# 2. correct `smime.pod` error


Error message is like below.

    
    installing man1/smime.1
    smime.pod around line 272: Expected text after =item, not a number
    smime.pod around line 276: Expected text after =item, not a number
    smime.pod around line 280: Expected text after =item, not a number
    smime.pod around line 285: Expected text after =item, not a number
    smime.pod around line 289: Expected text after =item, not a number
    POD document had syntax errors at /usr/bin/pod2man line 71.
    make: *** [install_docs] Error 255
    


Modify files:
`[parsec_root_dir]/pkgs/libs/ssl/src/doc/apps/smime.pod
[parsec_root_dir]/pkgs/libs/ssl/src/doc/ssl/SSL_COMP_add_compression_method.pod`
...
and so on.

Change `=item 0 `to `=item C<0>`

(Also other numbers as below.)

    
    268 =item C<0>
    269 
    270 the operation was completely successfully.
    271 
    272 =item C<1>
    273 
    274 an error occurred parsing the command options.
    275 
    276 =item C<2>
    277 
    278 one of the input files could not be read.
    279 
    280 =item C<3>
    281 
    282 an error occurred creating the PKCS#7 file or when reading the MIME
    283 message.
    284 
    285 =item C<4>
    286 
    287 an error occurred decrypting or verifying the message.
    288 
    289 =item C<5>
    290 
    291 the message was verified correctly but an error occurred writing out
    292 the signers certificates.
    


You can use following shell script. (in root directory of the benchmarks)

    
    #! /bin/bash
    for i in 0 1 2 3 4 5 6 7 8 9 
    do
        echo "Replacing '=item $i' to '=item C<$i>'"
        grep -rl "=item $i" * | xargs sed -i "s/=item $i/=item C<$i>/g"
    done





# 3. `__mbstate_t` conflict


Error message is like below.

    
    /usr/include/wchar.h:94:3: error: conflicting types for ‘__mbstate_t’
     } __mbstate_t;
       ^
    In file included from ../include/machine/bsd_endian.h:37:0,
                     from ../include/sys/bsd_types.h:44,
                     from ../include/sys/bsd_param.h:64,
                     from if_host.c:48:
    ../include/sys/bsd__types.h:105:3: note: previous declaration of ‘__mbstate_t’ was here
     } __mbstate_t;
    


It is because of conflict between system declaration and parsec library.

Comment out the declaration of `__mbstate_t` in parsec library:  `[parsec_root_dir]/pkgs/libs/uptcpip/src/include/sys/bsd__types.h
`(not `bsd_types.h`)

    
     96 /*
     97  * mbstate_t is an opaque object to keep conversion state during multibyte
     98  * stream conversions.
     99  */
    100 //#ifndef __mbstate_t_defined
    101 //# define __mbstate_t_defined    1
    102 //typedef union {
    103     //char      __mbstate8[128];
    104     //__int64_t _mbstateL;  [> for alignment <]
    105 //} __mbstate_t;
    106 //#endif 
    





<blockquote>

> 
> # ------------- Appended. November 4, 2015 ----------------
> 
> 
</blockquote>


According to the comment from Shwartz, following packages are needed to be installed on Ubuntu 14.04.1.

    
    sudo apt-get install -y build-essential m4 x11proto-xext-dev libglu1-mesa-dev libxi-dev libxmu-dev libtbb-dev



