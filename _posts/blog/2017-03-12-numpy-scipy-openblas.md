---
layout: post
title: Install scipy and numpy with openblas on Fedora 25
categories: blog
tags: [Coding]
author: diehlpk
---

## Compile [OpenBLAS](http://www.openblas.net/)
```BASH
tar -xvf OpenBLAS-0.2.19.tar.gz
cd OpenBLAS-0.2.19/
make BINARY=64 FC=gfortran USE_THREAD=4
mkdir /home/diehlpk/opt/openblas
make PREFIX=/home/diehlpk/opt/openblas install
```

## Configure and install numpy

```
pip install virtualenv
mkdir project
virtualenv project
source .pnumpy/bin/activate
mkdir .pddic/build
cd .pddic/build
git clone https://github.com/numpy/numpy.git numpy
unset CPPFLAGS
unset LDFLAGS
python setup.py build --fcompiler=gnu95
python setup.py install
```






