# rCUDA on ubuntu 16.04

This ansible script is supposed to install cuda and setup rCUDA afterwards.

## Start the rCUDAd
```
$ export LD_LIBRARY_PATH=/usr/local/cuda-8.0/targets/x86_64-linux/lib
$ ./rCUDAd -i
rCUDAd v18.03beta
Copyright 2009-2018 UNIVERSITAT POLITECNICA DE VALENCIA. All rights reserved.
Using TCP communications library.
rCUDAd[12487]: Using rCUDAcommTCP.so communications library.
rCUDAd[12487]: Server daemon succesfully started.
```

## Compile simple example

```
$ cd /usr/local/cuda-8.0/samples/1_Utilities/deviceQuery
$ export LD_LIBRARY_PATH=/usr/local/rCUDAv18.03beta-CUDA8.0-cuDNN6.0-linux64/lib
$ make EXTRA_NVCCFLAGS=--cudart=shared
/usr/local/cuda-8.0/bin/nvcc -ccbin g++ -I../../common/inc  -m64 --cudart=shared   -gencode arch=compute_20,code=sm_20 -gencode arch=compute_30,code=sm_30 -gencode arch=compute_35,code=sm_35 -gencode arch=compute_37,code=sm_37 -gencode arch=compute_50,code=sm_50 -gencode arch=compute_52,code=sm_52 -gencode arch=compute_60,code=sm_60 -gencode arch=compute_60,code=compute_60 -o deviceQuery.o -c deviceQuery.cpp
nvcc warning : The 'compute_20', 'sm_20', and 'sm_21' architectures are deprecated, and may be removed in a future release (Use -Wno-deprecated-gpu-targets to suppress warning).
/usr/local/cuda-8.0/bin/nvcc -ccbin g++   -m64 --cudart=shared     -gencode arch=compute_20,code=sm_20 -gencode arch=compute_30,code=sm_30 -gencode arch=compute_35,code=sm_35 -gencode arch=compute_37,code=sm_37 -gencode arch=compute_50,code=sm_50 -gencode arch=compute_52,code=sm_52 -gencode arch=compute_60,code=sm_60 -gencode arch=compute_60,code=compute_60 -o deviceQuery deviceQuery.o
nvcc warning : The 'compute_20', 'sm_20', and 'sm_21' architectures are deprecated, and may be removed in a future release (Use -Wno-deprecated-gpu-targets to suppress warning).
mkdir -p ../../bin/x86_64/linux/release
cp deviceQuery ../../bin/x86_64/linux/release
$ export RCUDA_DEVICE_COUNT=2
$ export RCUDA_DEVICE_0=127.0.0.1:0
$ export RCUDA_DEVICE_1=127.0.0.1:1
$ ./deviceQuery |grep ^Device
Device 0: "Tesla M60"
Device 1: "Tesla M60"
```
