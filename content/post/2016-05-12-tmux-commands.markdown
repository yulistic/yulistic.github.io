---
author: yulistic
comments: true
date: 2016-05-12 06:49:07+00:00
layout: post
link: http://yulistic.com/?p=264
slug: tmux-commands
title: tmux commands
wordpress_id: 264
language:
- English
topics:
- Tips
---

`tmux` is a useful tool:



	
  * to maintain sessions when ssh connection failed.

	
  * to make windows (tabs) and control them only with keyboard.

	
  * to make panes (split windows vertically or horizontally...) and control them only with keyboard.

	
  * and so on...




# Basic `tmux` commands


From out of the `tmux` session.



	
  * tmux new -s [session_name] : make a new session.

	
  * tmux ls : list current session list.


Inside of the `tmux` session. You should press Ctrl and b simultaneously for [Ctrl+b]. And the other keys follow.



	
  * [Ctrl + b] + $ : rename the current session.

	
  * [Ctrl + b] + c : make a new window. (You can find window information at the left bottom of the screen.)

	
  * [Ctrl + b] + , : rename the current window.

	
  * [Ctrl + b] + n : move to next window.

	
  * [Ctrl + b] + p : move to previous window.

	
  * [Ctrl + b] + [number] : move to [number]-th window.

	
  * [Ctrl + b] + % : split window (make a new pane) horizontally.

	
  * [Ctrl + b] + " : split window (make a new pane) vertically.

	
  * [Ctrl + b] + o : move to next pane

	
  * [Ctrl + b] + q + [number of pane] : move to the pane selected.

	
  * [Ctrl + d] : exit from current pane, window, or `tmux` session.



