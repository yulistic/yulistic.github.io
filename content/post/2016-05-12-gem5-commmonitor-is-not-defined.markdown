---
author: yulistic
comments: true
date: 2016-05-12 06:49:07+00:00
layout: post
link: http://yulistic.com/?p=251
slug: gem5-commmonitor-is-not-defined
title: '[Gem5] CommMonitor is not defined'
wordpress_id: 251
language:
- English
topics:
- Problems &amp; Solutions
---

# 1. Problem


While using CommMonitor in Gem5, the following error message prompted.

    
    Traceback (most recent call last):
      File "<string>", line 1, in <module>
      File "/home/yulistic/simulators/gem5/src/python/m5/main.py", line 388, in main
        exec filecode in scope
      File "configs/example/se_spec2006.py", line 285, in <module>
        system.monitor = CommMonitor(trace_file=trace_filename)
    NameError: name 'CommMonitor' is not defined




# 2. Cause


The error was because of absence of `protobuf`. When `scon` tried to compile `CommMonitor`, it checks whether the protobuf is installed or not. If it is not installed, `scon` skip `CommMonitor` compilation, so we cannot use it.

You can check warning messages which are prompted as yellow characters while building Gem5.

    
    yulistic@machine1:~/simulators/gem5$ scons build/X86/gem5.opt
    scons: Reading SConscript files ...
    Package protobuf was not found in the pkg-config search path.
    Perhaps you should add the directory containing `protobuf.pc'
    to the PKG_CONFIG_PATH environment variable
    No package 'protobuf' found
    Warning: pkg-config could not get protobuf flags.
    Checking for leading underscore in global variables...(cached) no
    Checking for C header file Python.h... (cached) yes
    Checking for C library pthread... (cached) yes
    Checking for C library dl... (cached) yes
    Checking for C library util... (cached) yes
    Checking for C library m... (cached) yes
    Checking for C library python2.7... (cached) yes
    Checking for accept(0,0,0) in C++ library None... (cached) yes
    Checking for zlibVersion() in C++ library z... (cached) yes
    Checking for GOOGLE_PROTOBUF_VERIFY_VERSION in C++ library protobuf... no
    Warning: did not find protocol buffer library and/or headers.
           Please install libprotobuf-dev for tracing support.




#  3. Solution


1) Download source package of `protobuf` from the [site](https://github.com/google/protobuf).

2) Install `protobuf.` Refer to the `README` file in the package.

3) Type command `protoc` that is a command for protocbuf compiler to check whether installation is completed.

4) If you get an error message like below, do

    
    sudo ldconfig


or

    
    export LD_LIBRARY_PATH=/usr/local/lib


5) After completing the installation of `protobuf`, rebuild gem5.

    
    scons build/X86/gem5.opt


It will not prompt warning message related to `protobuf` any more.


