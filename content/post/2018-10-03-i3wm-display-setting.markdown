---
title: "Display setting with i3wm"
date: 2018-10-03T17:19:21+09:00
author: "yulistic"
description: "How to apply display settings when using i3wm."
tags: ["Linux","i3wm","display settings"]
topics: ["issues"]
draft: false
---

# Problem
I'm using two monitors, and one of them is pivoted. The default display setting manager of `Manjaro` has an option for rotating view, but it was not applied when using `i3wm`.

# Solution
`xrands` was used. In a terminal, you can get the information of currently connected monitors with `xrands` without any options. (The following example shows the monitor status after applying settings.) 
```
$ xrands
Screen 0: minimum 320 x 200, current 5040 x 2620, maximum 16384 x 16384
DisplayPort-0 connected primary 3840x2160+0+0 (normal left inverted right x axis y axis) 941mm x 529mm
   3840x2160     60.00*+  29.98    24.00  
   2560x1440     59.95  
   2048x1080     59.99  
   1920x1080     60.00    60.00    50.00    59.94  
   1920x1080i    60.00    50.00    59.94  
   1680x1050     59.95  
   1280x1024     75.02    60.02  
   1440x900      74.98    59.89  
   1280x960      60.00  
   1280x720      60.00    59.94  
   1024x768      75.03    60.00  
   800x600       75.00    60.32  
   720x576       50.00  
   720x576i      50.00  
   720x480       60.00    59.94  
   720x480i      60.00    59.94  
   640x480       75.00    72.81    66.67    60.00    59.94  
   720x400       70.08  
HDMI-A-2 disconnected (normal left inverted right x axis y axis)
DVI-D-0 connected 1200x1920+3840+700 left (normal left inverted right x axis y axis) 518mm x 324mm
   1920x1200     59.95*+
   1920x1080     60.00  
   1600x1200     60.00  
   1680x1050     59.88  
   1280x1024     60.02  
   1280x960      60.00  
   1024x768      60.00  
   800x600       60.32  
   640x480       59.94  
   720x400       70.08  
HDMI1 disconnected (normal left inverted right x axis y axis)
HDMI2 disconnected (normal left inverted right x axis y axis)
VGA1 disconnected (normal left inverted right x axis y axis)
VIRTUAL1 disconnected (normal left inverted right x axis y axis)
```

You can change the display settings with options. I wanted to rotate the second monitor left and modify its vertical position to be matched with the primary monitor.

```
xrandr --output DVI-D-0 --rotate left --auto --pos 3840x700
```
The setting will be applied right after you enter the command.

This setting is not maintained after rebooting.  The command should be written in the file: `~/.xprofile` to be executed on startup.
