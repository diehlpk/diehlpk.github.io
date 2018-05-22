---
layout: post
title: Compile HPX with machine learning [HPXML](https://github.com/STEllAR-GROUP/hpxML) for run time optimization
categories: blog
tags: [Building]
author: diehlpk
---

### Prerequirements

1. [LLVM](http://releases.llvm.org/download.html) 
2. [CLANG](http://releases.llvm.org/download.html)
3. [HPX](https://github.com/STEllAR-GROUP/hpx) (Installation on [Ubuntu](https://diehlpk.github.io/blog/hpx-ubuntu-12.04/) and [Fedora](https://diehlpk.github.io/blog/hpx-fedora/))

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
wget wget http://releases.llvm.org/6.0.0/clang-tools-extra-6.0.0.src.tar.xz
tar -xvf clang-tools-extra-6.0.0.src.tar.xz
cd ..
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
make loop-convert
```

