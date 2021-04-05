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

* Install Python and dependencies with the following commands: 
```bash
sudo apt-get install python3-pip libprotoc-dev protobuf-compiler
pip3 --no-cache-dir install --upgrade \
setuptools \
        requests \
        easydict==1.9 \
        protobuf==3.8.0 \
        numpy==1.16.2 \
        pandas==0.22.0 \
        Pillow==6.2.0 \
        python-dateutil==2.8.1

pip3 --no-cache-dir install --upgrade \
setuptools \
        scipy==1.1.0 \
        onnx==1.5.0 \
        tqdm==4.25.0 \
        scikit-learn \
        Cython \
        opencv-python==3.4.5.20 \
        matplotlib==3.0.1
        
pip3 --no-cache-dir install --upgrade \
setuptools \
        libatlas-base-dev \
        libgflags-dev \
        libgoogle-glog-dev \
        libhdf5-serial-dev \
        libleveldb-dev \
        liblmdb-dev \
        libprotobuf-dev \
        libsnappy-dev \
        protobuf-compiler
        
pip3 --no-cache-dir install --upgrade \
setuptools \
        libatlas-base-dev \
        libgflags-dev \
        libgoogle-glog-dev \
        libhdf5-serial-dev \
        libleveldb-dev \
        liblmdb-dev \
        libprotobuf-dev \
        libsnappy-dev \
        protobuf-compiler \
        thop
```


* Install Cityscapes Scripts with the following commands: 
```bash
sudo git clone --depth 10 https://github.com/mcordts/cityscapesScripts ~/cityscapesScripts && \
    cd ~/cityscapesScripts && pip install .
```


* Install OpenCV with the following commands: 
```bash
sudo git clone --depth 10 --branch 3.4.5 https://github.com/opencv/opencv ~/opencv && \
    mkdir -p ~/opencv/build && cd ~/opencv/build && \
    cmake -D CMAKE_BUILD_TYPE=RELEASE \
          -D CMAKE_INSTALL_PREFIX=/usr/local \
          -D WITH_IPP=OFF \
          -D WITH_CUDA=OFF \
          -D WITH_OPENCL=OFF \
          -D BUILD_TESTS=OFF \
          -D BUILD_PERF_TESTS=OFF \
          .. && \
    make -j"$(nproc)" install && \
    ln -s /usr/local/include/opencv4/opencv2 /usr/local/include/opencv2
```


* Install PyTorch with the following commands: 
```bash
wget https://nvidia.box.com/shared/static/mmu3xb3sp4o8qg9tji90kkxl1eijjfc6.whl -O torch-1.1.0-cp36-cp36m-linux_aarch64.whl
sudo apt-get install python3-pip libopenblas-base libopenmpi-dev 
pip3 install torch-1.1.0-cp36-cp36m-linux_aarch64.whl
```
```bash
sudo apt-get install libjpeg-dev zlib1g-dev libpython3-dev libavcodec-dev libavformat-dev libswscale-dev
git clone --branch v0.3.0 https://github.com/pytorch/vision torchvision
cd torchvision
export BUILD_VERSION=0.3.0   
python3 setup.py install --user
```


* Install PyCuda with the following commands: 
```bash
python -m pip --no-cache-dir install \
        'pycuda>=2017.1.1'
```


* Clone FasterSeg-Repository: 
```bash
cd /home/ && git clone https://github.com/Gaussianer/FasterSeg.git
```
### Let's validate the installation using the latency test.

```bash
cd FasterSeg/latency
CUDA_VISIBLE_DEVICES=0 python3 run_latency.py
```

