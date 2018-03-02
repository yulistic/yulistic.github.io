---
author: yulistic
comments: true
date: 2016-05-12 06:49:06+00:00
type: post
link: http://yulistic.com/?p=114
slug: mint-linux-%ec%99%80%ec%9d%b8%ec%9c%bc%eb%a1%9c-%ec%8b%a4%ed%96%89%ed%95%9c-%ec%b9%b4%ec%b9%b4%ec%98%a4%ed%86%a1-%ed%95%9c%ea%b8%80-%ea%b9%a8%ec%a7%90%eb%ac%b8%ec%a0%9c-kakaotalk-cannot-display-kor
title: '[Mint Linux] English system locale에서 와인으로 실행한 카카오톡 한글 깨짐문제 (KakaoTalk cannot display Korean characters in English system locale.)'
language:
- English
topics:
- Issues
---

# Problem
시스템 로케일(language)를 English로 설정했을 때 와인으로 실행 중인 카카오톡 PC버전에서 한글이 깨지는 문제 발생. (ㅁㅁㅁㅁㅁㅁㅁ 이런 식으로 깨짐)  
I prefer to set my desktop system language(locale) as English. When the system locacle is changed to English, `KakaoTalk` messenger running on `Wine` does not display Korean correctly. It shows 'ㅁㅁㅁㅁㅁㅁ' instead of Korean characters. (There is no problem when the system language is set to Korean.)

# Environment
Mint Linux 17, Wine 1.7, System language (locale) = English  

# Solution
카카오톡의 프로그램만 Korean locale로 실행한다.  
Configure only `KakaoTalk` program to be run in Korean locale. (System locale is still English.)

즉, 카카오톡 실행아이콘을 텍스트편집기로 연 후, `Exec` 부분에 `env LANG=ko_KR.UTF-8`를 추가해준다. (command 앞 뒤로 한칸의 공백이 있어야 하며, wine command 앞에 위치해야 함)  
Open KakaoTalk icon with text editer (vi), add `env LANG=ko_KR.UTF-8` to `Exec` field. (Each command in `Exec` field should be separated with a white space. The inserted command should be located before 'wine ~~~' command.)

**Example)**
```
 Exec=env WINEPREFIX="/home/yulistic/.wine" env LANG=ko_KR.UTF-8 wine C:\\windows\\command\\start.exe /Unix /home/yulistic/.wine/dosdevices/
```




