---
layout:   post
title:    "安装 Intel Caffe"
subtitle: "Start with Intel Caffe"
date:     2019-05-27
author:   "Eric"
catalog:  true
header-img: "img/post/bg/post-bg-caffe.jpg"
tags:
  - Caffe
  - Intel
  - Deep Learning
---
> 官方的 caffe 难以安装，而 Intel 的 Caffe 不仅容易安装，而且经过了性能的调优。

## 1. 安装依赖
```sh
sudo apt-get update
sudo apt-get install build-essential cmake git \
    pkg-config libprotobuf-dev libleveldb-dev \
    libsnappy-dev libhdf5-serial-dev \
    protobuf-compiler libatlas-base-dev
sudo apt-get install --no-install-recommends libboost-all-dev
sudo apt-get install libgflags-dev \
    libgoogle-glog-dev liblmdb-dev \
    libopencv-dev
```

## 2. 下载 intel/caffe
```sh
git clone https://github.com/intel/caffe.git
```

## 3. 修改配置
```sh
cd caffe/
cp Makefile.config.example Makefile.config
```

配置文件 `Makefile.config` 中需要修改的地方
```sh
# 添加 /usr/include/hdf5/serial
INCLUDE_DIRS := $(PYTHON_INCLUDE) \
    /usr/local/include \
    /usr/include/hdf5/serial
# 添加 /usr/lib/x86_64-linux-gnu /usr/lib/x86_64-linux-gnu/hdf5/serial
LIBRARY_DIRS := $(PYTHON_LIB) \
    /usr/local/lib /usr/lib \
    /usr/lib/x86_64-linux-gnu \
    /usr/lib/x86_64-linux-gnu/hdf5/serial
```

## 4. 编译并测试
```sh
make all -j4
make test
make runtest
```

## 5. 编译 pycaffe
```sh
make pycaffe
```

