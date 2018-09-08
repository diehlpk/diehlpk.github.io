---
layout: post
title: Compile blazemark with HPX or OpenMP support
categories: blog
tags: [Building]
author: diehlpk
---

### Prerequirements

1. [HPX](https://github.com/STEllAR-GROUP)
2. [Blaze](https://bitbucket.org/blaze-lib/blaze/src/master/)


### Compile blazemark 

```bash
git clone https://bitbucket.org/blaze-lib/blaze/src/master/
cd blaze/balzemark
cp Configfile ConfigfileHPX
./configure ConfigfileHPX
make -j
```
### Using HPX

Add following lines to the ConfigfileHPX

```bash
CXX=clang++ or gcc
CXXFLAGS="-stdlib=libc++ -Wshadow -Woverloaded-virtual -O3 -std=c++17 -DNDEBUG -fpermissive -DBLAZE_USE_HPX_THREADS -isystem /home/pdiehl/opt/hpx/include -Wl,-wrap=main"
INCLUDE_DIRECTIVES="-isystem /home/pdiehl/opt/hpx/include" 
LIBRARY_DIRECTIVES="-llapack -L/home/pdiehl/opt/hpx/lib/ -lhpx -lhpx_wrap   -rdynamic /home/pdiehl/opt/hpx/lib/libhpx_init.a /home/pdiehl/opt/hpx/lib/libhpx.    so -ldl -lrt -L/opt/boost/1.67.0-clang6.0.0/release/lib -lboost_system -lboost_program_options "
```

### Using OpenMP

Add following lines to the ConfigfileHPX

```bash
CXX=clang++ or gcc
CXXFLAGS="-Wall -Wextra -Werror -Wshadow -Woverloaded-virtual -ansi -O3 -march=native -std=c++14 -DNDEBUG -fpermissive -fopenmp"
LIBRARY_DIRECTIVES="-llapack"                                                    
```
