---
layout: post
title: Compile HPX directly on the Raspberry Pi 3
categories: blog
tags: [Building]
author: diehlpk
---

### Prerequirements

1. Install [Fedora Arm](https://fedoraproject.org/wiki/Architectures/ARM/Raspberry_Pi#Downloading_the_Fedora_ARM_image) on the Micro SDK card 
2. Configure your Pi by connecting it to a screen and follow the installation routine.
3. Generate a 4Gb swap partion.

### Install dependencies

```bash
dnf install boost-devel hwloc-devel cmake git gperftools-devel gcc-c++ automake make
```

### Compile HPX

```bash
cmake -DHPX_WITH_GENERIC_CONTEXT_COROUTINES=ON ..
make -j 1
```

### Generate rpm package for distribution on other Pis

```bash
dnf install rpm-build 
```


```bash
cmake  -DHPX_WITH_GENERIC_CONTEXT_COROUTINES=ON  -DHPX_WITH_RPM=ON ..
make package
```




