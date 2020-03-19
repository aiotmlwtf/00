---
title: bootstrap
description: starting from scratch with the nvidia nano jetson
published: 1
date: 2020-03-19T12:15:18.911Z
tags: 
---

---

**goal**: GPU-accelerated docker setup
experiment with
nvidia-docker, jupyter, conda, tf, pytorch, cuda, opencl, deepspeech, nemo-asr


**Jetson Nano**
cpu: ARMv8
SD image: Ubuntu 18.04 LTS port (with native x64 support)
user space apps / kernel arch are aarch64 / arm64 (64-bit)



### prep

```bash
sudo apt-get update
sudo apt-get install nano screen curl apt-utils
```

### l4t (linux for tegra)

![jetson_bsp_architecture.png](/jetson_bsp_architecture.png){.align-center}
[jetson board support architecture](https://docs.nvidia.com/jetson/archives/l4t-archived/l4t-3231/index.html) + module description
[l4t packages](https://docs.nvidia.com/jetson/archives/l4t-archived/l4t-3231/index.html#page/Tegra%2520Linux%2520Driver%2520Package%2520Development%2520Guide%2Fquick_start.html%23wwpID0EVHA)
[nano software features](https://docs.nvidia.com/jetson/archives/l4t-archived/l4t-3231/index.html#page/Tegra%2520Linux%2520Driver%2520Package%2520Development%2520Guide%2Fsoftware_features_jetson_nano.html%23wwconnect_header)

### docker

https://github.com/NVIDIA/nvidia-docker/wiki
https://github.com/NVIDIA/nvidia-docker/wiki/NVIDIA-Container-Runtime-on-Jetson
https://github.com/collabnix/dockerlabs/tree/master/beginners/install/jetson-nano

nvidia-docker  https://www.youtube.com/watch?v=-Y4T71UDcMY


https://devblogs.nvidia.com/gpu-containers-runtime/
```bash
# update docker 18.09 to 19.03
curl -sSL https://get.docker.com/ | sh
sudo docker version
sudo usermod -aG docker ai
```

### conda
https://github.com/Archiconda/build-tools/releases
https://github.com/Archiconda/build-tools/releases/tag/0.2.3
click/download:
Archiconda3-0.2.3-Linux-aarch64.sh
$ bash Archiconda3-0.2.3-Linux-aarch64.sh

install/use Archiconda on a Jetson Nano inside Docker:
https://github.com/helmuthva/jetson/blob/master/workflow/deploy/ml-base/src/Dockerfile

Overall "ml-base" project:
https://github.com/helmuthva/jetson

Docker Image including Jupyter notebooks in the "jupyter" image:
https://github.com/helmuthva/jetson/blob/master/workflow/deploy/jupyter/src/Dockerfile
The build instructions in the Dockerfiles can be easily replicated on the host in case you don't want to use Docker.


### tf/keras docker

https://github.com/Tony607/jetson_nvidia_dockers
https://www.dlology.com/blog/how-to-run-keras-model-on-jetson-nano-in-nvidia-docker-container/
```
sudo docker pull docker.io/zcw607/jetson:r1.0.1
sudo docker run --runtime nvidia --network host -it -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix zcw607/jetson:r1.0.1
```





### NeMo **Neural Modules Toolkit**

Neural Modules toolkit for conversational AI, speech and NLP networks.
Collections of ASR, NLP and TTS modules representing data layers, encoders, decoders, language models, loss functions, or methods of combining activations. 

NeMo allows the combination and re-use of those building blocks (while providing a level of semantic correctness checking via its neural type system). 

Pretrained models: **Jasper, Quartznet, Transformer, Tacotron2, Waveglow**

```
docker pull nvcr.io/nemo/nemo_asr_app_img:v1.0
wget https://ngc.nvidia.com/catalog/models/nvidia:quartznet15x5
wget https://ngc.nvidia.com/catalog/models/nvidia:wsj_quartznet_15x5
```

https://ngc.nvidia.com/catalog/containers/nvidia:nemo
```
sudo docker pull nvcr.io/nvidia/nemo:v0.9

sudo docker run --runtime=nvidia -it --rm -v --shm-size=8g -p 8888:8888 -p 6006:6006 --ulimit memlock=-1 --ulimit stack=67108864 nvcr.io/nvidia/nemo:v0.9

sudo docker run --runtime=nvidia -it --rm -v <nemo_github_folder>:/NeMo --shm-size=8g -p 8888:8888 -p 6006:6006 --ulimit memlock=-1 --ulimit stack=67108864 nvcr.io/nvidia/nemo:v0.9
```


**Pytorch**
apex extension: https://github.com/NVIDIA/apex

```
sudo docker pull nvcr.io/nvidia/pytorch:20.02-py3
sudo docker run --runtime nvidia --network host -it -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix nvcr.io/nvidia/l4t-base:r32.3.1
```




---

### deep learning SDK
https://developer.nvidia.com/deep-learning-software
The Deep Learning SDK requires [CUDA Toolkit](https://developer.nvidia.com/cuda-toolkit)


### NVIDIA SDK Manager / JetPack

https://developer.nvidia.com/embedded/jetpack
sdk manager [installing NVIDIA Jetson SDK Manager](https://www.youtube.com/watch?v=s1QDsa6SzuQ)

**notes**
- probably easier to just flash the sd card, instead of doing it through the sdk manager
- a nvidia account is needed to download the sdk
- a dedicated [ubuntu installation](https://ubuntu.com/download/desktop) (eg. a [usb flash drive](https://linuxhint.com/run-ubuntu-18-04-from-usb-stick/)) to run [nvidia's sdk manager](https://developer.nvidia.com/nvidia-sdk-manager) is recommended
- 8 GB of memory (and a full-HD screen) are required according to NVIDIA, but if 8GB is not available, go to the settings tab (upper-right of sdk manager), lower the number of concurrent downloads and threads per downloads (slow but possible)

**installs**
- CUDA Toolkit for L4T - c/c++ gpu-acceleration libraries)
- NVIDIA container runtime - docker integration 0.9.0
- cuDNN - CUDA library with DL primitives
- TensorRT
fast inference engine, inference runtime for production deployment using INT8/FP16 optimized precision which reduces latency
- OpenCV
- Multimedia API: high-level (gstreamer) and lower-level media apis
- DeepStream SD
C++ API/runtime/toolkit for transcoding, streaming video analytics, inference (situational awareness) through computer vision, intelligent video analysis (IVA) and multi-sensor processing
- VisionWorks
- VPI
- DALI: input data processing
- NCCL: multi-GPU communication routines
- Optical Flow SDK: video inference, stereo disparity calculation, depth estimation
- Transfer Learning Toolkit: SDK for tuning domain specific DNNs
- AI-Assisted Annotation SDK: for medical imaging
- DIGITS: DL GPU training system for image classification, segmentation and object detection - = - cuBLAS: GPU-accelerated Linear Algebra functionality
- cuSPARSE: subroutines for sparse matrices, eg. for natural language processing
- Automatic Mixed Precision speedup

### various

```bash
cp -r /usr/local/cuda/bin/cuda-install-samples-10.0.sh /home/ai
```

- jetson headless: disable ubuntu desktop

```bash
# the screen will turn black
sudo systemctl enable ssh && sudo systemctl isolate multi-user.target

log in via ssh

# if you like your nano this way you can make the change persist after reboot
sudo systemctl set-default multi-user.target
```
### install kernel sources 

[link](https://devtalk.nvidia.com/default/topic/1055416/request-install-linux-headers-on-jetson-nano/?offset=9)
https://developer.nvidia.com/embedded/dlc/nv-sdk-manager
find sources_sync.sh in the install path in a subfolder called 'Linux for tegra'
```
./source_sync.sh -k tegra-l4t-r32.1
```
