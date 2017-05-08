+++
author = "yulistic"
date = "2017-05-08T14:56:44+09:00"
description = "ctags option tips"
draft = false
tags = ["ctags"]
title = "ctags tips"
topics = ["tips"]
type = "post"

+++

* Use `--exclude` option to exclude some directories or files from a `ctags` build.

```bash
ctags -R --exclude="build"
```

* Python could be traversed with the option `--python-kindes=-i`

```bash
ctags -R --python-kinds=-i
```




