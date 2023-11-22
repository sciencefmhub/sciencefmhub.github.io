---
title: "Docker"
linkTitle: "Docker"
weight: 35
description: >
  Cybertraining Links
tags:
- rivanna
- docker
---



Docker drivers images from NVIDIA



## Install GPU drivers in a docker image

NVIDIA GPU drivers can be installed into docker images.
As the software may frequently cange, we recommend to look at
the [Nvidia documentation](https://nvidia.github.io/nvidia-container-runtime)

An example to add to a debian based Dockerfile to install the GPU drivers (this may be incomplete and you need to check the instructions):

```
RUN curl -s -L https://nvidia.github.io/nvidia-container-runtime/gpgkey | \
    apt-key add - \ &&
    distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \ &&
    curl -s -L https://nvidia.github.io/nvidia-container-runtime/$distribution/nvidia-container-runtime.list | 
RUN apt-get update \ &&
apt-get install -y nvidia-container-runtime
```

* <https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#debian-installation>

* <https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html>
