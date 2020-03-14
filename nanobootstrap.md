---
title: bootstrap
description: starting from scratch with the nvidia nano jetson
published: 1
date: 2020-03-14T16:43:07.043Z
tags: 
---

Surface area

In order to perform optimized machine learning tasks, the jetson nano needs to be populated with drivers and libraries, which also have to co-operate with python libraries like numpy, scipy, pycuda, pytorch etc. etc. 
This (anno20200314) proved to be cumbersome here (ymmv) using just gcc, apt-get and pip

Goal is to obtain a (docker) setup to experiment with **nvidia-docker, tf, pytorch, cuda, opencl, nemo-asr, jupyter, python3 and other things DL**

---
video: [installing NVIDIA Jetson SDK Manager, JetPack 2.2](https://www.youtube.com/watch?v=s1QDsa6SzuQ)

notes:
- a nvidia account is needed to download the sdk
- a dedicated [ubuntu installation](https://ubuntu.com/download/desktop) (eg. a [usb flash drive](https://linuxhint.com/run-ubuntu-18-04-from-usb-stick/)) to run [nvidia's sdk manager](https://developer.nvidia.com/nvidia-sdk-manager) is recommended
- 8 GB of memory (and a full-HD screen) are required according to NVIDIA, but if 8GB is not available, go to the settings tab (upper-right of sdk manager), lower the number of concurrent downloads and threads per downloads (slow but possible)

**Installables:**
- CUDA Toolkit for L4T - c/c++ gpu-acceleration libraries)
- cuDNN - CUDA Deep Neural Network library
- TensorRT - fast inference using INT8/FP16 optimized precision which reduces latency
- OpenCV
- VisionWorks
- VPI
- NVIDIA container runtime - docker integration 0.9.0
- Multimedia API - high-level (gstreamer) and lower-level media apis
- DeepStream SDK - streaming analytics toolkit for situational awareness through computer vision, intelligent video analysis (IVA) and multi-sensor processing

---


nvidia-docker https://www.youtube.com/watch?v=-Y4T71UDcMY


---
jetson headless: disable ubuntu desktop

```bash
# the screen will turn black
sudo systemctl enable ssh && sudo systemctl isolate multi-user.target

log in via ssh

# if you like your nano this way you can make the change persist after reboot
sudo systemctl set-default multi-user.target




---
??? To install kernel sources (on a fresh Ubuntu 18 install), see: 
https://developer.nvidia.com/embedded/dlc/nv-sdk-manager

find sources_sync.sh in the install path in a subfolder called 'Linux for tegra'
./source_sync.sh -k tegra-l4t-r32.1

[link](https://devtalk.nvidia.com/default/topic/1055416/request-install-linux-headers-on-jetson-nano/?offset=9)
