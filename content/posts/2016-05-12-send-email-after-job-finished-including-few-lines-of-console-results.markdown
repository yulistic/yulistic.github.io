---
author: yulistic
comments: true
date: 2016-05-12 06:49:07+00:00
type: post
link: http://yulistic.com/?p=221
slug: send-email-after-job-finished-including-few-lines-of-console-results
title: Send email after job finished (including few lines of console results)
wordpress_id: 221
language:
- English
topics:
- Tips
---

# Purpose


Want to be notified remotely when a job has been finished (through email).

Also, include a few lines of final results (`stdout` a.k.a. console output) as the content of the email.


# Solution


Use `tee` command to make additional file with the content of `stdout`.

Use `tail` command to get a few lines of the last printed output after the job finished.

    
    <job command> | tee <console output file path>; tail <console output file path> | mail -s "<mail title>" <mail address>


For example,

    
    scons build/X86/gem5.opt | tee ~/temp/output.out; tail ~/temp/output.out | mail -s "gem5 X86 build completed" abc@abc.com





