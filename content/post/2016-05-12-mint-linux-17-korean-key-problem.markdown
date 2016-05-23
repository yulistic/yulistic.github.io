---
author: yulistic
comments: true
date: 2016-05-12 06:49:06+00:00
layout: post
link: http://yulistic.com/?p=104
slug: mint-linux-17-korean-key-problem
title: '[Mint Linux 17] Korean key problem'
wordpress_id: 104
language:
- English
tags:
- linux
- mint
topics:
- Problems &amp; Solutions
---

Mint Linux 17 한영키 문제
Mint Linux 17 Korean/English convert key problem.

시스템 환경: Mint Linux 17 64bit
Environment: Mint Linux 17 64bit

문제: ibus, nabi 등을 이용해 보았지만, Chromium 브라우저에서의 한글 문제를 해결하기 까다로움.
Problem: I cannot use "Korean/English convert key" in Chromium browser on Mint Linux 17.

해결: 결국 uim-byeoru 입력기를 이용하여 문제 해결.
Solution: Use "uim-byeoru" input method.

자세한 사항:
Details:

1. Software Manager를 이용하던지(추천), apt install uim-byeoru를 터미널에서 입력하여 uim-byeoru를 설치.
Install uim-byeoru with Software Manager or typing "apt install uim-byeoru" at Terminal. (It is recommended to use Software Manager.)

2. uim을 기본 Input Method로 설정. (아래 그림 참고)
Set  "uim"  as default Input Method. (Refer to following screenshot.)

[caption id="attachment_105" align="aligncenter" width="666"][![input method](http://yulistic.com/wp-content/uploads/2014/08/input_method.png)](http://yulistic.com/wp-content/uploads/2014/08/input_method.png) input method[/caption]



3. uim-byeoru의 setting을 변경.
Change uim-byeoru settings.

[caption id="attachment_106" align="aligncenter" width="673"][![uim byeoru setting](http://yulistic.com/wp-content/uploads/2014/08/uim-input-method.png)](http://yulistic.com/wp-content/uploads/2014/08/uim-input-method.png) uim byeoru setting[/caption]



"Input method deployment"를 체크해주고 "Default input method"를 "byeoru"로 선택해준다.
Check "input method deployment", set "Default input method" as "byeoru"

[caption id="attachment_107" align="aligncenter" width="802"][![uim settings](http://yulistic.com/wp-content/uploads/2014/08/uim-pref-gtk_009.png)](http://yulistic.com/wp-content/uploads/2014/08/uim-pref-gtk_009.png) uim settings[/caption]



[Byeoru] on / [Byeoru] off에 Edit을 이용하여 "hangul"을 추가해준다. 한자도 바꾸어준다. (이 때 Mint Linux의 키보드 setting이 "Korean (101/104 key compatible)" 이어야 "hangul"과 "hangul-hanja"로 키가 잡힌다. Preferences > Keyboard > Keyboard layout에서 확인할 것.)
Add "hangul" to "[Byeoru] on" and "[Byeoru] off" clicking "Edit..." button. Set also "Chinese characters" as "hangul-hanja". (Prerequisite: "Korean (101/104 key compatible)" should be set as system default keyboard layout. Check it in "Preferences > Keyboard > Keyboard layout")

[caption id="attachment_109" align="alignnone" width="802"][![](http://yulistic.com/wp-content/uploads/2014/08/uim-setting-21.png)](http://yulistic.com/wp-content/uploads/2014/08/uim-setting-21.png) uim settings 2[/caption]



4. 모든 사항을 저장하고 시스템 재부팅 하면 한영키가 올바르게 작동하는 것을 확인할 수 있다.
Save all and reboot the  system.




