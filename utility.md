---
title: Utility
description: bits of handy something
published: 1
date: 2020-03-11T16:11:43.787Z
tags: 
---

### search in git repositories
https://grep.app


### access jetson (xterm/code-oss/notebook) from your laptop

**access jetson's jupyter notebook**
- prepare
```bash
# generate jupyter config file (/home/ai/.jupyter/jupyter_notebook_config.py)
jupyter notebook --generate-config

# at the end of the config file, add:
c.NotebookApp.allow_origin = '*' 	#	allow all origins
c.NotebookApp.ip = '0.0.0.0' 			# listen to all IPs

# you *may need to open the default jupyter port on the firewall: tcp:8888, eg, ufw
sudo ufw allow 8888 

jupyter notebook password # set a password

jupyter notebook 				 		# start jupyter
jupyter notebook xxx.ipynb 	# idem with a notebook
```
- connect: http://ai0x.local:8888/login?

- file tree: http://ai0x.local:8888/tree


**access jetson's code-oss (code editor)**
- prepare
```bash

# server side (on the jetson)
nano /etc/ssh/sshd_config

# add at end of file (or find parameters with Ctrl-W)
X11Forwarding yes
# I also set these, not sure if they're all needed here
AllowAgentForwarding yes
AllowTcpForwarding yes
X11Forwarding yes
TCPKeepAlive yes

# set unique hostname on jetson
hostname ai0x
```
- connect and open code-oss
```bash
ssh -Y ai@ai0x.local -C code-oss -n
# -n : force new window
```

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