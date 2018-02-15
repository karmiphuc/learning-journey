---
layout: post
summary: "In big loops, isset() is better than strlen()"
tags: programming php
---
> Source: http://jpauli.github.io/2015/01/22/on-php-function-calls.html

Basically, it concludes with:

```php

if (strlen($name) > 49) {
...
}

```

..._**being about 20% slower**_ than...

```php

if (isset($name[49])) {
...
}

```

...in a big loop, which is perfectly normal.

#### Why such a result?

It's not the way strlen() computes the length that's in cause. Because the length of every PHP string is always known when strlen() is called. A big part of such lengths are even computed at compile time, when possible. PHP encapsulates the length of the string into the C structure carrying a PHP string, when it creates such string into memory. So strlen() just reads that little info, and returns it to you as-is. In fact, strlen() is probably the fastest PHP function that exists. It just does nothing in term of computation. Here is its source code:

```c

ZEND_FUNCTION(strlen)
{
    char *s1;
    int s1_len;

    if (zend_parse_parameters(ZEND_NUM_ARGS() TSRMLS_CC, "s", &s1, &s1_len) == FAILURE) {
        return;
    }

    RETVAL_LONG(s1_len);
}

```

Knowing that isset() is not a function, the ~20% perf penalty of strlen() over isset() is mainly brought by the overhead of a function call in the Zend Engine.

There is another thing to say as well: comparing the result of strlen() with something, adds an extra OPCode, whereas using just an isset(), represents one unique OPCode.

Here is the if(strlen()) construct disassembled:

```asm

line     #* I O op                           fetch          ext  return  operands
-----------------------------------------------------------------------------------
   3     0  >   SEND_VAR                                                 !0
         1      DO_FCALL                                      1  $0      'strlen'
         2      IS_SMALLER                                       ~1      42, $0
         3    > JMPZ                                                     ~1, ->5
   5     4  > > JMP                                                      ->5
   6     5  > > RETURN                                                   1
   
```

And here is the semanticaly equivalent if(isset()) structure disassembled:

```asm

line     #* I O op                           fetch          ext  return  operands
-----------------------------------------------------------------------------------
   3     0  >   ISSET_ISEMPTY_DIM_OBJ                       33554432  ~0      !0, 42
         1    > JMPZ                                                  ~0, ->3
   5     2  > > JMP                                                       ->3
   6     3  > > RETURN                                                     1

```

As you can see, there is no function call involved into the isset() code (DO_FCALL), as well as there is no IS_SMALLER OPCode (just ignore the RETURN statements). isset() will directly return a boolean for evaluation, whereas strlen() will return a temporary variable, passed to IS_SMALLER OPCode, and only this OPCode result will be evaluated by the if(). That's two OPCodes for the strlen() code structure and only one for the isset() one, which lets us smell that the isset() structure will also be faster because of this fact. (computing two operations is usually slower that computing just one).
