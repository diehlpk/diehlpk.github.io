---
layout: post
title: Compile HPX with machine learning HPXML for run time optimization
categories: blog
tags: [Building]
author: diehlpk
---

### Prerequirements

1. [LLVM](http://releases.llvm.org/download.html) 
2. [CLANG](http://releases.llvm.org/download.html)
3. Install [libeigen](http://eigen.tuxfamily.org/index.php?title=Main_Page)
Note that LLVM and CLANG need to be compiled to intstall the clang tool for HPXML

### Install llvm

```bash
module load clang/6.0.0
wget http://releases.llvm.org/6.0.0/llvm-6.0.0.src.tar.xz
tar -xvf llvm-6.0.0.src.tar.xz
cd llvm-6.0.0.src/ && mkdir build && cd build
cmake -DCMAKE_BUILD_TYPE=Release -DLLVM_TARGETS_TO_BUILD="X86" ..
make -j
```

### Install clang

```bash
export PATH=/home/pdiehl/Compile/llvm-6.0.0.src/build/bin/:$PATH
wget http://releases.llvm.org/6.0.0/cfe-6.0.0.src.tar.xz
tar -xvf cfe-6.0.0.src.tar.xz
cd cfe-6.0.0.src/ 
cd tools
mkdir extra && cd extra
wget http://releases.llvm.org/6.0.0/clang-tools-extra-6.0.0.src.tar.xz
tar -xvf clang-tools-extra-6.0.0.src.tar.xz
cp -r clang-tools-extra-6.0.0.src/* .
cd ../..
mkdir build && cd build
cmake -DCMAKE_BUILD_TYPE=Release ..
make -j 
```

### Install clang tool

```bash
mkdir ../tools/extra/loop-convert
cp ../../hpxML/ClangTool/LoopConvert.cpp ../tools/extra/loop-convert
cp ../../hpxML/ClangTool/CMakeLists.txt ../tools/extra/loop-convert
echo 'add_subdirectory(loop-convert)' >> ../tools/extra/CMakeLists.txt
cmake ..
make loop-convert
```

### Paramters

#### Install [libeigen](http://eigen.tuxfamily.org/index.php?title=Main_Page)

```bash
wget http://bitbucket.org/eigen/eigen/get/3.3.4.tar.gz
tar -xvf 3.3.4.tar.gz
cd eigen-eigen-5a0156e40feb && mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX=/home/pdiehl/opt/eigen
make -j 
```

#### Compile tool for obtaining the parameters

```bash
export CXX=/home/pdiehl/Compile/cfe-6.0.0.src/build/bin/clang++
export CC=/home/pdiehl/Compile/cfe-6.0.0.src/build/bin/clang
export CPLUS_INCLUDE_PATH=/opt/mn/clang/6.0.0/include/c++/v1/:$CPLUS_INCLUDE_PATH
export LIBRARY_PATH=/home/pdiehl/Compile/llvm-6.0.0.src/build/lib/:$LIBRARY_PATH
cd logisticRegressionModel/algorithms/ && mkdir build
cmake -DEigen3_DIR=/home/pdiehl/opt/eigen/share/eigen3/cmake/ ..
make 
cd ../..
```

### HPXML

For installing the dependencies of [HPX](https://github.com/STEllAR-GROUP/hpx) on [Ubuntu](https://diehlpk.github.io/blog/hpx-ubuntu-12.04/) or [Fedora](https://diehlpk.github.io/blog/hpx-fedora/)) look here.

```bash
module load boost/1.67.0-clang6.0.0-release
cd hpxml
cmake ..
make core 
```

Note, that you have to use the your own builded clang compiler with the clang tool.
