# Install-FasterSeg-on-a-Xavier-Jetson
This repository contains installation instructions to get FasterSeg running on a Jetson Xavier. 
So far, this installation has only checked the latency tests. Possibly dependencies for other scripts of FasterSeg are still missing. 

## Prerequisites
- JetPack 4.3

## Installation

### Installation of the required tools to perform the installation of the dependencies
* Install the following tools with the following command: 
```bash
sudo apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        apt-utils \
        ca-certificates \
        wget \
        git \
        vim \
        libssl-dev \
        curl \
        unzip \
        unrar \
        libsm6 \
        libxext6 \
        libxrender-dev
```

* Install CMake with the following command: 
```bash
git clone --depth 10 https://github.com/Kitware/CMake ~/cmake && \
    cd ~/cmake && \
    ./bootstrap && \
    make -j"$(nproc)" install
```
