---
layout: post
title: Install scipy and numpy with intel_mkl on Fedora 25
categories: blog
tags: [Coding]
author: diehlpk
---

## Requirements

* [Virtualenv](https://pypi.python.org/pypi/virtualenv)
```bash
pip install virtualenv 
```
* Intel compilers and mkl library
 
## Configure and install [numpy](http://www.numpy.org/)

```bash
mkdir .pnumpy
virtualenv .pnumpy
source .pnumpy/bin/activate
pip install Cython
mkdir .pnumpy/build
cd .pnumpy/build
git clone https://github.com/numpy/numpy.git numpy
cd numpy
cp site.cfg.example site.cfg
```

Open the site.cfg with your favorite text editor and uncomment following lines and add the paths fitting to your system

```yaml
[mkl]
library_dirs = /usr/local/intel/mkl/lib/intel64
include_dirs = /usr/local/intel/mkl/include/
lapack_libs = mkl_def, mkl_intel_lp64, mkl_gnu_thread, mkl_core, mkl_mc3
```

After that run this line to compile and install numpy with the icc and intel_mkl 


```bash
export CFLAGS='-fopenmp -O2 -march=core2 -ftree-vectorize'
export LDFLAGS='-lm -lpthread -lgomp'
python setup.py config --compiler=intelem build_clib --compiler=intelem build_ext --compiler=intelem install
```

## Configure and install [scipy](https://www.scipy.org/)

```bash
export LDFLAGS="${LDFLAGS} -shared"
git clone https://github.com/scipy/scipy.git
cd scipy
python setup.py config --compiler=intelem build_clib --compiler=intelem build_ext --compiler=intelem install
```

## Usage
With `OMP_NUM_THREADS` you can specifiy how many threads should be used, when numpy or scipy can execute the method in parallel. 

```bash
source .pnumpy/bin/activate
export OMP_NUM_THREADS=4
python script.py
```
