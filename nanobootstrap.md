---
title: bootstrap
description: starting from scratch with the nvidia nano jetson
published: 1
date: 2020-03-14T12:32:07.506Z
tags: 
---

Surface area

In order to perform optimized machine learning tasks, the jetson nano needs to be populated with drivers and libraries, which also have to co-operate with python libraries like numpy, scipy, pycuda, pytorch etc. etc. 
This (anno20200314) proved to be cumbersome here (ymmv) using just gcc, apt-get and pip

Goal is to obtain a (docker) setup to experiment with **nvidia-docker, tf, pytorch, cuda, opencl, nemo-asr, jupyter, python3 and other things DL**


---

Let's dedicate a [ubuntu installation](https://ubuntu.com/download/desktop) (eg. a [usb flash drive](https://linuxhint.com/run-ubuntu-18-04-from-usb-stick/)) to run [nvidia's sdk manager](https://developer.nvidia.com/nvidia-sdk-manager) and install proper graphics drivers, kernel extensions etcetera from there[.](https://devtalk.nvidia.com/default/topic/1055416/request-install-linux-headers-on-jetson-nano/?offset=9)

To install kernel sources (on a fresh Ubuntu 18 install), see: 
https://developer.nvidia.com/embedded/dlc/nv-sdk-manager
find sources_sync.sh in the install path in a subfolder called 'Linux for tegra'
./source_sync.sh -k tegra-l4t-r32.1


---
