+++
author = "Jongyul Kim"
date = "2016-05-25T10:58:46+09:00"
description = "Auto load the cscope database file (cscope.out) from subdirectories."
keywords = ["cscope", "autoload"]
tags = ["cscope", "autoload", "srcexpl"]
title = "Autoload Cscope Database"
topics = ["issues"]
type = "post"

+++

# Problem
`Vim` could not find the `cscope` db file (`cscope.out`) from any subdirectories of the project root. Although I could use `cscope` by accessing all the files from the project root directory, some plugins (`SrcExpl`) set `autochdir` option to be on automatically. Once the option was turned on, I could not use `cscope` any more with the error message like 'Cannot find file.'

# Solution
* Reference: [Autoloading Cscope Database](http://vim.wikia.com/wiki/Autoloading_Cscope_Database)

As mentioned in the reference site, the problem could be solved by adding the following script to the `~/.vimrc` file which is the usual `vim` configuration file.

```
# ~/.vimrc file.
function! LoadCscope()
  let db = findfile("cscope.out", ".;")
  if (!empty(db))
    let path = strpart(db, 0, match(db, "/cscope.out$"))
    set nocscopeverbose " suppress 'duplicate connection' error
	exe "cs add " . db . " " . path
	set cscopeverbose
  endif
endfunction
au BufEnter /* call LoadCscope()

```

