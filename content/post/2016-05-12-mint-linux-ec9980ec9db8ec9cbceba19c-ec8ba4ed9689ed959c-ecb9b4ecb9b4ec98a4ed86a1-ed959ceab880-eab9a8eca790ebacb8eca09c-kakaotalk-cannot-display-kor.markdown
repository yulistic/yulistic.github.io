---
author: yulistic
comments: true
date: 2016-05-12 06:49:06+00:00
type: post
link: http://yulistic.com/?p=114
slug: mint-linux-%ec%99%80%ec%9d%b8%ec%9c%bc%eb%a1%9c-%ec%8b%a4%ed%96%89%ed%95%9c-%ec%b9%b4%ec%b9%b4%ec%98%a4%ed%86%a1-%ed%95%9c%ea%b8%80-%ea%b9%a8%ec%a7%90%eb%ac%b8%ec%a0%9c-kakaotalk-cannot-display-kor
title: '[Mint Linux] 와인으로 실행한 카카오톡 한글 깨짐문제 (KakaoTalk cannot display Korean characters.)'
wordpress_id: 114
language:
- English
topics:
- Issues
---

# Problem
와인으로 돌린 카카오톡의 한글이 ㅁㅁㅁㅁㅁㅁㅁ 이런 식으로 깨짐. 우선 시스템 language를 korean으로 바꾸면, 한글이 잘 표시되나, english로 했을 경우에는 깨짐.  
KakaoTalk running on Wine cannot display Korean. It displays Korean characters as 'ㅁㅁㅁㅁㅁㅁ'.

# Environment
Mint Linux 17, Wine 1.7, System language (locale) = english  

# Solution
카카오톡의 프로그램만 korean locale로 실행되도록 한다.  
Configure KakaoTalk runs in Korean locale.

카카오톡 실행아이콘을 텍스트편집기로 연 후, `Exec` 부분에 `env LANG=ko_KR.UTF-8`를 추가해준다. (command 앞 뒤로 한칸의 공백이 있어야 하며, wine command 앞에 위치해야 함)  
Open KakaoTalk icon with text editer (vi), add `env LANG=ko_KR.UTF-8` to `Exec` field. (Each command in `Exec` field should be separated with space. The command being inserted should be located before 'wine ~~~' command.)

**Example)**
```
 Exec=env WINEPREFIX="/home/yulistic/.wine" env **LANG=ko_KR.UTF-8** wine C:\\windows\\command\\start.exe /Unix /home/yulistic/.wine/dosdevices/
```




