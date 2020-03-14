---
title: bootstrap
description: starting from scratch with the nvidia nano jetson
published: 1
date: 2020-03-14T11:42:01.114Z
tags: 
---

### from scratch(-ing the surface)

reading some, it seems best to dedicate a [ubuntu installation](https://ubuntu.com/download/desktop) ([usb flash drive](https://linuxhint.com/run-ubuntu-18-04-from-usb-stick/)) and run [nvidia's sdk manager](https://developer.nvidia.com/nvidia-sdk-manager) from there. It'll hopefully be easier to populate a nano with graphics drivers, kernel extensions, and other needed things.

goal:
obtain a setup for easy experimenting with **nvidia-docker, tf, pytorch, cuda, nemo-asr**

---

install kernel sources on a fresh Ubuntu 18 install
see: https://developer.nvidia.com/embedded/dlc/nv-sdk-manager
find sources_sync.sh in the install path in a subfolder called Linux for tegra

`./source_sync.sh -k tegra-l4t-r32.1`

[link](https://devtalk.nvidia.com/default/topic/1055416/request-install-linux-headers-on-jetson-nano/?offset=9)