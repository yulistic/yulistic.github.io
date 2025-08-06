+++
author = "yulistic"
date = "2018-03-16T15:02:43+09:00"
description = "How to crop pdf file with pdf-crop-margins maintaining the PDF meta data. Additionally, do it without enormous file size growing."
draft = false
tags = ["pdf","crop", "pdf-crop-margins", "pdfcrop"]
title = "Crop pdf keeping information and size"
topics = ["tips"]
type = "post"

+++

# Intro.
I use Sony `DPT-RP1` (a.k.a. Digital Paper) as a paper reader.
In spite of the 13.3-inch-big screen of this device, large margins of pdf files made my eyes tired.
I wanted to crop pdf files with the following requirements.

1. Meta data like a title and authors should be maintained after being cropped.
2. The size of cropped file should be reasonable (similar to the original file).
3. Some components in the pdf file need to be cropped out. (For example, page numbers at the bottom.)

I used `pdfcrop` tool before. It was easy to use and the output was acceptable but the size of file increases unexpectedly (e.g. 600KB to 5MB).

# Solution
`pdf-crop-margins` python tool was great for me. You can get the detailed information from the [official site](https://pypi.python.org/pypi/pdfCropMargins/0.1.3).

## Install
It is assumed that `pip` is installed in your PC.
```
sudo pip install pdfCropMargins
```

## Usage
I used `pdfCropMargins` as below.
```
pdf-crop-margins -ap4 45 49 45 49 -p 100 AAA.pdf -o AAA_cropped.pdf
```
`pdf-crop-margins` crops out margins of a pdf file with the default configuration.
The result with this default configuration also nice but the third requirement was not satisfied in my case.

With `-ap4` (pre-crop) option, I could crop out the page number and adjust to fit my device's screen perfectly.  
With `-p 100` option, it does not crop further after the pre-cropping.
