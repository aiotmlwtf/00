---
title: nanobootstrap
description: nvidia nano jetson / docker installation notes
published: 1
date: 2020-03-19T17:54:43.506Z
tags: installation
---

*goal*


GPU-accelerated docker setup(s) for <span style="color:#f00;font-weight:800;">
jupyter/conda, tf, pytorch, cuda, opencl, deepspeech, nemo-asr</span>, etc.

<details>
<summary>prepare</summary>
  
```bash
sudo apt-get update
sudo apt-get install nano screen curl apt-utils
sudo apt-get install libffi-dev python-openssl

sudo apt-get install libnvidia-container-tools nvidia-container-runtime
sudo apt-get install cuda*
more ?
```
</details>


<div style="background-color:#eee;">

 <details>
<summary>Jetson Nano Board</summary>

  cpu: ARMv8
SD image: Ubuntu 18.04 LTS port (with native x64 support)
user space apps / kernel arch are aarch64 / arm64 (64-bit)

### l4t (linux for tegra)

![jetson_bsp_architecture.png](/jetson_bsp_architecture.png){.align-center}
[jetson board support architecture](https://docs.nvidia.com/jetson/archives/l4t-archived/l4t-3231/index.html) + module description
[l4t packages](https://docs.nvidia.com/jetson/archives/l4t-archived/l4t-3231/index.html#page/Tegra%2520Linux%2520Driver%2520Package%2520Development%2520Guide%2Fquick_start.html%23wwpID0EVHA)
[nano software features](https://docs.nvidia.com/jetson/archives/l4t-archived/l4t-3231/index.html#page/Tegra%2520Linux%2520Driver%2520Package%2520Development%2520Guide%2Fsoftware_features_jetson_nano.html%23wwconnect_header)
</details>
</div>

<div style="background-color:#eee;">
<details>
<summary>SDK's</summary>

Deep Learning SDK requires [CUDA Toolkit](https://developer.nvidia.com/cuda-toolkit)
https://developer.nvidia.com/deep-learning-software


NVIDIA SDK Manager / JetPack
https://developer.nvidia.com/embedded/jetpack

[installing NVIDIA Jetson SDK Manager](https://www.youtube.com/watch?v=s1QDsa6SzuQ)
**notes**
This is just for reference, it's easier to just flash the sd card, instead of doing it through the sdk manager.

- a nvidia account is needed to download the sdk
- a dedicated [ubuntu installation](https://ubuntu.com/download/desktop) (eg. a [usb flash drive](https://linuxhint.com/run-ubuntu-18-04-from-usb-stick/)) to run [nvidia's sdk manager](https://developer.nvidia.com/nvidia-sdk-manager) is recommended
- 8 GB of memory (and a full-HD screen) are required according to NVIDIA, but if 8GB is not available, go to the settings tab (upper-right of sdk manager), lower the number of concurrent downloads and threads per downloads (slow but possible)
- there's a bug in the partitioning, so after flashing (over usb-eth), the 13 l4t partitions need to be moved to the end of the sdcard (so root can be resized to use all space)

**installs**

- NVIDIA container runtime - docker integration 0.9.0
- OpenCV
- VisionWorks
- VPI
- DALI: input data processing
- NCCL: multi-GPU communication routines  
- CUDA Toolkit for L4T - c/c++ gpu-acceleration libraries)
- cuDNN - CUDA library with DL primitives
- TensorRT - fast inference enginefor production deployment using INT8/FP16 optimized precision (reduced latency)
- Multimedia API: high-level (gstreamer) and lower-level media apis
- DeepStream SDK
  C++ API/runtime/toolkit for transcoding, streaming video analytics, inference (situational awareness) through computer vision, intelligent video analysis (IVA) and multi-sensor processing
- Optical Flow SDK: video inference, stereo disparity calculation, depth estimation
- Transfer Learning Toolkit: SDK for tuning domain specific DNNs
- AI-Assisted Annotation SDK: for medical imaging
- DIGITS: DL GPU training system for image classification, segmentation and object detection 
- cuBLAS: GPU-accelerated Linear Algebra functionality
- cuSPARSE: subroutines for sparse matrices, eg. for natural language processing
- Automatic Mixed Precision speedup
</details>
</div>








<div style="background-color:#0cf;">
<details>
<summary>Docker</summary>

  ```bash
# update docker 18.09 to 19.03
curl -sSL https://get.docker.com/ | sh
sudo docker version
sudo usermod -aG docker ai
```

```
  # tests
docker run hello-world
docker run arm64v8/hello-world
docker run -it ubuntu bash
docker container run alpine echo "Hello World"
docker container run arm64v8/alpine echo "Hello World"
```

**nvidia-docker**
  
*l4t*: use container l4t-base:r32.2 for nvidia docker on Jetson ('exec format error' upon running an image indicates usage of unsupported image(x86) on the ARM system)
the **l4t-base** docker image enables l4t applications to be run in a container. It has the necessary contents of the l4t rootfs included within. The platform specific libraries and select device nodes for a particular device are mounted by the NVIDIA container runtime into the l4t-base container from the underlying host, thereby providing necessary dependencies for l4t applications to execute within the container. This approach enables the l4t-base container to be shared between various Jetson devices. **CUDA and TensorRT are ready to use within the l4t-base container** as they are made available from the host by the NVIDIA container runtime.  

[nvidia-docker wiki](https://github.com/NVIDIA/nvidia-docker/wiki)
https://docs.nvidia.com/jetson/l4t/index.html
[l4t-base docker container](https://ngc.nvidia.com/catalog/containers/nvidia:l4t-base)
https://devblogs.nvidia.com/gpu-containers-runtime
[nvidia-docker setup](https://www.youtube.com/watch?v=-Y4T71UDcMY) - access GPU within Docker containers (youtube)
[jetson nano install](https://github.com/collabnix/dockerlabs/tree/master/beginners/install/jetson-nano)
[NVIDIA Container Runtime on Jetson](https://github.com/NVIDIA/nvidia-docker/wiki/NVIDIA-Container-Runtime-on-Jetson)
  
```bash
# allow external applications to connect to the host's X display
xhost +
# allow root user access to running X server
#xhost +si:localuser:root
xhost +si:ai:root  

docker pull nvcr.io/nvidia/l4t-base:r32.3.1

# start a GPU-enabled container  
# docker run --runtime nvidia --network host -it -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix nvcr.io/nvidia/l4t-base:r32.3.1

OK:
docker run -it --rm --net=host --runtime nvidia --gpus all -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix nvcr.io/nvidia/l4t-base:r32.3.1

NO:
docker run -it --gpus all -p 5000:5000 nvidia/digits

NO:
docker run --runtime=nvidia --rm -it gcr.io/tensorflow/tensorflow:latest-gpu bash
# https://marmelab.com/blog/2018/03/21/using-nvidia-gpu-within-docker-container.html
docker run --runtime=nvidia --rm -it -v "${PWD}:/app" gcr.io/tensorflow/tensorflow:latest-gpu python /app/benchmark.py cpu 10000
  
  
# docker run -it --rm --net=host --runtime=nvidia --shm-size=1g -e NVIDIA_VISIBLE_DEVICES=0 --rm nvcr.io/nvidia/pytorch:18.05-py3
  
  
  
  
# -it				run in interactive mode
# --rm			delete the container when finished
# --runtime nvidia 	use the NVIDIA container runtime while running the l4t-base container

# --device  mount additional devices
# -v 				mounting directory, bind mount directories and files, also used to mount host’s X11 display in the container filesystem to render video output

# r32.3.1 	tag for the image corresponding to the l4t release 32.3.1
# -d				daemonize

```

  
[building cuda in containers on jetson](https://github.com/NVIDIA/nvidia-docker/wiki/NVIDIA-Container-Runtime-on-Jetson#building-cuda-in-containers-on-jetson)
NVIDIA Container Runtime by default supports use of a limited set of device nodes and associated functionality within the l4t-base containers.
https://github.com/NVIDIA/nvidia-docker/wiki/NVIDIA-Container-Runtime-on-Jetson
</details>

<details>
<summary>docker-compose</summary>

**Dockerfile**

```bash
FROM python:3.7-alpine
WORKDIR /code
ENV FLASK_APP app.py
ENV FLASK_RUN_HOST 0.0.0.0
RUN apk add --no-cache gcc musl-dev linux-headers
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
COPY . .
CMD ["flask", "run"]  
```
    
**docker-compose.yml**
  
```yaml
version: '3'
services:
  web:
    build: .
    ports:
      - "5000:5000"
  redis:
    image: "redis:alpine"
``` 

**requirements.txt**

```bash
flask
redis
```
  
**run*

```bash
docker-compose up
docker-compose up -d
docker-compose down
```
  
</details>

  
  
  
  
  
</details>
  
</div>

<div style="background-color:#fac;">
<details>
  <summary>Jupyter & Conda</summary>

**install/use Archiconda on a Jetson Nano inside Docker**
https://forums.developer.nvidia.com/t/anaconda-for-jetson-nano/74286
https://github.com/Archiconda/build-tools/releases
https://github.com/Archiconda/build-tools/releases/tag/0.2.3

  click/download:
Archiconda3-0.2.3-Linux-aarch64.sh
$ bash Archiconda3-0.2.3-Linux-aarch64.sh
  
Docker Image including Jupyter notebooks in the "jupyter" image:
https://github.com/helmuthva/jetson/blob/master/workflow/deploy/jupyter/src/Dockerfile
The build instructions in the Dockerfiles can be easily replicated on the host in case you don't want to use Docker.

https://github.com/helmuthva/jetson/blob/master/workflow/deploy/ml-base/src/Dockerfile
Overall "ml-base" project:
https://github.com/helmuthva/jetson
 </details>
</div>


<div style="background-color:#000;">
<details>
  <summary>tensorflow, keras, docker</summary>
  
https://github.com/Tony607/jetson_nvidia_dockers
https://www.dlology.com/blog/how-to-run-keras-model-on-jetson-nano-in-nvidia-docker-container/
  
```
sudo docker pull docker.io/zcw607/jetson:r1.0.1
sudo docker run --runtime nvidia --network host -it -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix zcw607/jetson:r1.0.1
```
</details>
</div>

<div style="background-color:#000;">
<details>
  <summary>NeMo - Neural Modules Toolkit</summary>
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
  </details>
  </div>  
  
<div style="background-color:#000;">
<details>
  <summary>pytorch</summary>
  
  apex extension: https://github.com/NVIDIA/apex

```
sudo docker pull nvcr.io/nvidia/pytorch:20.02-py3
```


  </div>
  </details>
  
  
  <details><summary>various</summary>
  
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
  
http://www.ironspider.ca/format_text/fontstyles.htm
  </details>
  
