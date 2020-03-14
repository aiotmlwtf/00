---
title: bootstrap
description: starting from scratch with the nvidia nano jetson
published: 1
date: 2020-03-14T10:59:13.697Z
tags: 
---


Starting from scratch, goal is to have a setup for easy experimenting with nvidia-docker and several docker images for deep learning. After reading some [forum post](https://devtalk.nvidia.com/default/topic/1055416/request-install-linux-headers-on-jetson-nano/?offset=9), it seems best to dedicate a [ubuntu installation](https://ubuntu.com/download/desktop) ([usb flash drive](https://linuxhint.com/run-ubuntu-18-04-from-usb-stick/)) and run [nvidia's sdk manager](https://developer.nvidia.com/nvidia-sdk-manager) from there to populate a running nano with drivers and kernel extensions.

other links:
https://developer.nvidia.com/embedded/dlc/nv-sdk-manager

note: 
To install kernel sources (needed later for compilation)
```
./source_sync.sh -k tegra-l4t-r32.1
```



