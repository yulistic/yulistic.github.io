+++
author = "yulistic"
date = "2017-08-31T11:08:28+09:00"
description = "Exporting to cropped png image in LibreOffice Draw"
draft = false
tags = ["Draw","LibreOffice", "export", "png", "crop"]
title = "Exporting to a cropped png image in LibreOffice 5 Draw"
topics = ["tips"]
type = "post"

+++


# Problem
I wanted to export a figure drawn with LibreOffice Draw to png file.
The two requirements below were my consideration.

1. The exported image should have transparent background.
2. The whitespace of page should be cropped out. Namely, the exported image should fit to the figure it contains.

# Solution
Following instructions will lead you to export a right image.

1. Check `Tools > Options > LibreOffice > General > Open/Save Dialogs > Use LibreOffice dialogs`.
2. Select all your image. You can use shourtcut, `Ctrl+a`.
3. `File > Export` will show you a dialog in which you can check `Selection`.
4. Enter file name, select format as PNG, check `Selection` and click `Export...`.
5. `PNG Options` dialog will be displayed. Check `Save transparency` for transparent background.

After click confirm, you will get a png file as you want.
