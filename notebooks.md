---
title: notebooks
description: 
published: 1
date: 2020-03-29T01:26:05.604Z
tags: 
---


--- 
<span style="background-color:#0c0; font-size: 16px;">
  
  [aiotmlwtf collab file](https://colab.research.google.com/drive/1sGN0DJSlKNzfi7-FYYwG42rcDu0PgaYN) 
</span>

[nano](https://aiotmlwtf.xyz/nanobootstrap)


[older](https://aiotmlwtf.xyz/collab_links)


---

# jetson access

<span style="background-color:#0c0; font-size: 16px;">
  running jetson's jupyter/code-oss from another computer
</span>

### prepare
```bash
#set jetson's unique hostname
sudo hostname ai0x

# also set it to ai0x here:
sudo nano /etc/hostname
```

## **jupyter notebook**
### prepare
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
### connect to jupyter
```bash
http://ai0x.local:8888/login?

# file tree
http://ai0x.local:8888/tree
```

## **code-oss (code editor)**
### prepare
```bash
# on the jetson, at the end of
nano /etc/ssh/sshd_config
# add these lines (or find the parameters in the file and change to):
X11Forwarding yes
TCPKeepAlive yes
# possibly not needed
AllowTcpForwarding yes
AllowAgentForwarding yes
```
### connect and open code-oss
```bash
ssh -Y ai@ai0x.local -C code-oss -n
# -n : force new window
```
