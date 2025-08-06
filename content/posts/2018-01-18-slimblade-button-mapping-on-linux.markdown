+++
author = "yulistic"
date = "2018-01-18T19:14:03+09:00"
description = "Kensington Slimblade trackball button mapping on Fedora using evdev"
tags = ["Linux","slimblade", "mouse button mapping", "evdev"]
title = "Kensington Slimblade button mapping on Linux"
topics = ["linux"]
type = "post"
+++

# Intro.

There are four buttons on the [Kensington Slimblade](https://www.kensington.com/en/ae/4493/k72327eu/slimblade-trackball) trackball mouse. I wanted to use the left-top button as `Backward` button and the right-top one as `Forward`.
There would be some other solutions for mouse button mapping, but I used `evdev` which operates on a `X11` layer.

# Solution
Add following lines to the file: `/usr/share/X11/xorg.conf.d/10-evdev.conf`.

```
# Kensington Slimblade Settings

Section "InputClass"
Identifier "Kensington Slimblade Trackball"
MatchProduct "Kensington Slimblade Trackball"
MatchIsPointer "on"
MatchDevicePath "/dev/input/event*"
Driver "evdev"

Option "ButtonMapping" "1 8 3 4 5 6 7 9"

EndSection

```

The key line is `Option "ButtonMapping" "1 8 3 4 5 6 7 9 2"`. The final string indecates that it will map the button `1` to `1`, `2` to `8`, `3` to `3`, and so on. (The position number to the described number).

Use `xev` tool to figure out the number of each button on your mouse.

In my case, I was helped with the other mouse to get the number of a `Backward` button and a `Forward` button. Those were `8` and `9` respectively.

Finally, I could map the left-top button(2) to `Backward` button(8) and the right-top button(8) to `Forward` button(9).
