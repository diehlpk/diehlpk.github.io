---
layout: post
title: Building Peridigm 1.4.1 on Fedora 23
categories: blog
tags: [Building]
author: diehlpk
---

<h1>Installing packages</h1>
{% highlight bash %}
sudo dnf mpich-devel mpich netcdf-mpich-devel netcdf-mpich hdf5-mpich-devel hdf5-mpich netcdf-fortran-mpich-devel boost-mpich-devel boost-mpich blas-devel blas lapack-devel lapack gcc-c++
{% endhighlight %}
{% highlight bash %}
sudo dnf  groupinstall "X Software Development"
{% endhighlight %}


<h1>Load the mpich module</h1>
{% highlight bash %}
module load mpi/mpich-x86_64
{% endhighlight %}

<h1>Building <a href="https://trilinos.org/download/">Trilinos</a> (trilinos-12.0.6)</h1>
{% highlight bash  %}
wget https://github.com/trilinos/Trilinos/archive/trilinos-release-12-0-1.tar.gz
tar -xf trilinos-release-12-0-1.tar.gz
cd trilinos-release-12-0-1
mkdir build && cd build
cmake \
-D CMAKE_INSTALL_PREFIX:PATH=/home/diehl/local/trilinos-12.0.6 \
-D CMAKE_CXX_FLAGS:STRING="-O2 -ansi -pedantic -ftrapv -Wall -Wno-long-long" \
-D CMAKE_BUILD_TYPE:STRING=RELEASE \
-D Trilinos_WARNINGS_AS_ERRORS_FLAGS:STRING="" \
-D Trilinos_ENABLE_ALL_PACKAGES:BOOL=OFF \
-D Trilinos_ENABLE_Teuchos:BOOL=ON \
-D Trilinos_ENABLE_Shards:BOOL=ON \
-D Trilinos_ENABLE_Sacado:BOOL=ON \
-D Trilinos_ENABLE_Epetra:BOOL=ON \
-D Trilinos_ENABLE_EpetraExt:BOOL=ON \
-D Trilinos_ENABLE_Ifpack:BOOL=ON \
-D Trilinos_ENABLE_AztecOO:BOOL=ON \
-D Trilinos_ENABLE_Amesos:BOOL=ON \
-D Trilinos_ENABLE_Anasazi:BOOL=ON \
-D Trilinos_ENABLE_Belos:BOOL=ON \
-D Trilinos_ENABLE_ML:BOOL=ON \
-D Trilinos_ENABLE_Phalanx:BOOL=ON \
-D Trilinos_ENABLE_Intrepid:BOOL=ON \
-D Trilinos_ENABLE_NOX:BOOL=ON \
-D Trilinos_ENABLE_Stratimikos:BOOL=ON \
-D Trilinos_ENABLE_Thyra:BOOL=ON \
-D Trilinos_ENABLE_Rythmos:BOOL=ON \
-D Trilinos_ENABLE_MOOCHO:BOOL=ON \
-D Trilinos_ENABLE_TriKota:BOOL=OFF \
-D Trilinos_ENABLE_Stokhos:BOOL=ON \
-D Trilinos_ENABLE_Zoltan:BOOL=ON \
-D Trilinos_ENABLE_Piro:BOOL=ON \
-D Trilinos_ENABLE_Teko:BOOL=ON \
-D Trilinos_ENABLE_SEACASIoss:BOOL=ON \
-D Trilinos_ENABLE_SEACAS:BOOL=ON \
-D Trilinos_ENABLE_SEACASBlot:BOOL=ON \
-D Trilinos_ENABLE_Pamgen:BOOL=ON \
-D Trilinos_ENABLE_EXAMPLES:BOOL=OFF \
-D Trilinos_ENABLE_TESTS:BOOL=ON \
-D TPL_ENABLE_Matio=OFF \
-D TPL_ENABLE_HDF5:BOOL=ON \
-D TPL_ENABLE_Netcdf:BOOL=ON \
-D TPL_ENABLE_MPI:BOOL=ON \
-D TPL_ENABLE_BLAS:BOOL=ON \
-D TPL_ENABLE_LAPACK:BOOL=ON \
-D TPL_ENABLE_Boost:BOOL=ON \
-D CMAKE_VERBOSE_MAKEFILE:BOOL=OFF \
-D Trilinos_VERBOSE_CONFIGURE:BOOL=OFF \
-D Netcdf_INCLUDE_DIRS=/usr/include/mpich-x86_64/ \
-D HDF5_INCLUDE_DIRS=/usr/include/mpich-x86_64/ \
..
{% endhighlight %}
After the configuration with CMake run
{% highlight bash  %}
make -j
make install
{% endhighlight %}
to build and install Trilinos.

<h1>Building <a href="https://peridigm.sandia.gov/">Peridigm</a> (1.4.1) </h1>
Get [Peridigm](https://github.com/peridigm/peridigm) from github
{% highlight bash %}
git clone https://github.com/peridigm/peridigm.git
git fetch
git checkout release-1.4.1
cd peridigm 
mkdir build
cd build
{% endhighlight %}
Now execute CMake in the generated build folder
{% highlight bash %}
cmake \
-D CMAKE_BUILD_TYPE:STRING=Release \
-D Trilinos_DIR:PATH=/home/diehl/local/trilinos-12.0.6/lib/cmake/Trilinos/ \
-D CMAKE_C_COMPILER:STRING=/usr/lib64/mpich/bin/mpicc \
-D CMAKE_CXX_COMPILER:STRING=/usr/lib64/mpich/bin/mpicxx \
-D CMAKE_CXX_FLAGS:STRING="-O2 -Wall -ansi -pedantic -Wno-long-long -ftrapv -Wno-deprecated -std=gnu++11" \
..
{% endhighlight %}
Now run 
{% highlight bash %}
make  -j
./src/Peridigm
{% endhighlight %}
to build and run Peridigm.

For a more detailed [description](http://iltabiai.github.io/peridynamics/fedora/tips/2016/04/20/Peridigm141-Fedora23.html) read [Ilyass Tabiai](https://twitter.com/joydisee)'s blog.

