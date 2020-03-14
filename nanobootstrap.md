---
title: bootstrap
description: starting from scratch with the nvidia nano jetson
published: 1
date: 2020-03-14T20:10:07.434Z
tags: 
---


nvidia-docker  https://www.youtube.com/watch?v=-Y4T71UDcMY
sdk manager [installing NVIDIA Jetson SDK Manager, JetPack 2.2](https://www.youtube.com/watch?v=s1QDsa6SzuQ)

---
obtain a (docker) setup to experiment with **nvidia-docker, tf, pytorch, cuda, opencl, nemo-asr, jupyter, python3 and other things DL**

---
```bash
sudo apt-get install nano screen curl apt-utils
cp -r /usr/local/cuda/bin/cuda-install-samples-10.0.sh /home/ai
# update docker to 19.03
curl -sSL https://get.docker.com/ | sh
sudo usermod -aG docker ai
```

```
sudo docker run --runtime nvidia --network host -it -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix nvcr.io/nvidia/l4t-base:r32.3.1
```

**Pytorch**
apex extension: https://github.com/NVIDIA/apex
```
docker pull nvcr.io/nvidia/pytorch:20.02-py3
```
**Neural Modules Toolkit**
Neural Modules toolkit for conversational AI, speech and NLP networks, collections of ASR, NLP and TTS modules. Modules represent data layers, encoders, decoders, language models, loss functions, or methods of combining activations. NeMo provides the combinination and re-use of building blocks while providing a level of semantic correctness checking via its neural type system. 
- pretrained models: **Jasper, Quartznet, Transformer(attention is all you need), Tacotron2, Waveglow**


```
sudo docker pull nvcr.io/nvidia/nemo:v0.9

sudo docker run --runtime=nvidia -it --rm -v --shm-size=8g -p 8888:8888 -p 6006:6006 --ulimit memlock=-1 --ulimit stack=67108864 nvcr.io/nvidia/nemo:v0.9
sudo docker run --runtime=nvidia -it --rm -v <nemo_github_folder>:/NeMo --shm-size=8g -p 8888:8888 -p 6006:6006 --ulimit memlock=-1 --ulimit stack=67108864 nvcr.io/nvidia/nemo:v0.9
```


```
docker pull nvcr.io/nemo/nemo_asr_app_img:v1.0
wget https://ngc.nvidia.com/catalog/models/nvidia:quartznet15x5
wget https://ngc.nvidia.com/catalog/models/nvidia:wsj_quartznet_15x5
```


---
jetson headless: disable ubuntu desktop

```bash
# the screen will turn black
sudo systemctl enable ssh && sudo systemctl isolate multi-user.target

log in via ssh

# if you like your nano this way you can make the change persist after reboot
sudo systemctl set-default multi-user.target
```


### NVIDIA SDK Manager

notes:
- a nvidia account is needed to download the sdk
- a dedicated [ubuntu installation](https://ubuntu.com/download/desktop) (eg. a [usb flash drive](https://linuxhint.com/run-ubuntu-18-04-from-usb-stick/)) to run [nvidia's sdk manager](https://developer.nvidia.com/nvidia-sdk-manager) is recommended
- 8 GB of memory (and a full-HD screen) are required according to NVIDIA, but if 8GB is not available, go to the settings tab (upper-right of sdk manager), lower the number of concurrent downloads and threads per downloads (slow but possible)

**Installed are:**
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
To install kernel sources (on a fresh Ubuntu 18 install), see: 
https://developer.nvidia.com/embedded/dlc/nv-sdk-manager
find sources_sync.sh in the install path in a subfolder called 'Linux for tegra'
./source_sync.sh -k tegra-l4t-r32.1

[link](https://devtalk.nvidia.com/default/topic/1055416/request-install-linux-headers-on-jetson-nano/?offset=9)
