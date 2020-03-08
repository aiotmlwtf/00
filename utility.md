---
title: Utility
description: bits of handy something
published: 1
date: 2020-03-08T23:02:29.829Z
tags: 
---


## search in git repositories
https://grep.app

## get a terminal on the jetson

```bash
# first set unique hostname on nano
hostname ai0x

# on laptop
ssh -Y ai@ai0x.local -C xterm

```

## convert decimal to binary/hexadecimal

<span style="color:#f00;">python has built in functions for base conversion<span>
  
``` python
print("decimal=%d, binary=%d, hexadecimal=%d" % ( 42, bin(42), hex(42) ))

# but if you need to specify the amount of digits
def getBinaryString(x, n=0): return format(x, 'b').zfill(n)

# as lambda function
getBinaryString = lambda x, n: format(x, 'b').zfill(n)

>>> bin(3)
'0b11'
>>> getBinaryString(3)
'11'
>>> getBinaryString(3,4)
'0011'

```
arguments:
x : int - decimal number to convert
n : int - min digits, if x needs less digits in binary, the rest is zeropadded
returns: String