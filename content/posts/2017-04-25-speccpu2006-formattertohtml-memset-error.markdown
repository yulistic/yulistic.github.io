+++
author = "yulistic"
date = "2017-04-25T00:03:27+09:00"
Description = "Issue for compiling 483.xalancbmk."
draft = false
tags = ["speccpu2006"]
Title = "Speccpu2006 FormatterToHTML.cpp memset was not declared error"
topics = ["issues"]
type = "post"

+++

# Problem

Error occurs while compiling SPECCPU2006 benchmark, `483.xalancbmk` with following messages.

```
FormatterToHTML.cpp: In member function 'void xalanc_1_8::FormatterToHTML::initCharsMap()':                                                                     
FormatterToHTML.cpp:139:42: error: 'memset' was not declared in this scope      
Specmake: *** [FormatterToHTML.o] Error 1  
```

The problem was because `string` library was not included in `FormatterToHTML.cpp` file.

## Solution

One possible solution might be to add one line of code, `#include <cstring>` to the `FormatterToHTML.cpp` file.
But, SPECCPU2006 benchmark checks MD5 before the compilation, which prompts another error for the one-line modifying solution.

Fortunately, a compiler option provides an interface to include library without the source code modification.
You can add the options `-include cstdlib -include cstring` to your config file to solve the problem as below.
```
...

483.xalancbmk=default=default=default:
CXXPORTABILITY = -DSPEC_CPU_LINUX -include cstdlib -include cstring
...

```

Done.
