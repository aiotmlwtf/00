---
title: Utility
description: bits of handy something
published: 1
date: 2020-03-12T19:47:35.778Z
tags: 
---

### search in git repositories
https://grep.app




### news (ml/dev/math)
[hackernews](https://hn.algolia.com/?dateRange=all&page=0&prefix=false&query=machine%20learning&sort=byDate&type=story)
https://devurls.com
https://mathurls.com

### cmdline
https://www.commandlinefu.com/commands/browse
https://onlinelinuxtools.com

### convert/parse/encode/decode
https://www.browserling.com/tools/html-to-markdown
https://onlineunicodetools.com/?msg11
(xml/html/yaml/csv/bin etc.)

### curl cookbook
https://catonmat.net/cookbooks/curl




### convert decimal to binary/hexadecimal

<span style="color:#f00;">python has built in functions for base conversion<span>
  
``` python
print("decimal=%d, binary=%d, hexadecimal=%d" % ( 42, bin(42), hex(42) ))

# to specify the amount of digits  
def getBinaryString(x, n=0): return format(x, 'b').zfill(n)

# as lambda function
getBinaryString = lambda x, n: format(x, 'b').zfill(n)

#x : int - decimal number to convert
#n : int - min digits, if x needs less digits in binary, the rest is zeropadded
#returns: String  

>>> bin(3)
'0b11'
>>> getBinaryString(3)
'11'
>>> getBinaryString(3,4)
'0011'

```