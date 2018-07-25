---
layout: post
title: Building Peridigm on Ubuntu 16.04
categories: blog
tags: [Building]
author: diehlpk
---

## Requirements

* zlib  (Ubuntu package)
* curl (Ubuntu package)
* libblas-dev (Ubuntu package)
* liblapack-dev (Ubuntu package)

## Bulding [OpenMPI](https://www.open-mpi.org/software/ompi/v2.1/) 2.0.1
{% highlight bash %}
wget https://download.open-mpi.org/release/open-mpi/v2.1/openmpi-2.1.0.tar.gz
tar -xf openmpi-2.1.0.tar.gz
cd cd openmpi-2.0.1
mkdir build && cd build
../configure --prefix=/home/diehl/local/openmpi-2.0.1
make -j
make install
cd ../..
{% endhighlight %}
Export path for the usage of the new compiler
{% highlight bash %}
export CC=/home/diehl/local/openmpi-2.0.1/bin/mpicc 
export CXX=/home/diehl/local/openmpi-2.0.1/bin/mpicxx
export CF=/home/diehl/local/openmpi-2.0.1/bin/mpif90 
export FC=/home/diehl/local/openmpi-2.0.1/bin/mpif90 
export F77=/home/diehl/local/openmpi-2.0.1/bin/mpif77
export LIBRARY_PATH=/home/diehl/local/openmpi-2.0.1/lib/:${LIBRARY_PATH}
export PATH=/home/diehl/local/openmpi-2.0.1/bin/:$PATH
{% endhighlight %}

## Bullding [Boost](http://www.boost.org/users/download/) 1.62.0
{% highlight bash %}
wget https://dl.bintray.com/boostorg/release/1.67.0/source/boost_1_67_0.tar.gz
tar -xf boost_1_67_0.tar.gz
cd boost_1_67_0
echo "using mpi ;" >> user-config.jam
./bootstrap.sh --prefix=/home/diehl/local/boost-1.62
./b2 --layout=tagged -j 
./b2 install
cd ..
{% endhighlight %}

## Building [HDF5](https://www.hdfgroup.org/downloads/index.html) (hdf5-1.8.15-patch1)
{% highlight bash %}
wget https://support.hdfgroup.org/ftp//HDF5/prev-releases/hdf5-1.8/hdf5-1.8.15-patch1/src/hdf5-1.8.15-patch1.tar
tar -xf hdf5-1.8.15-patch1.tar
cd hdf5-1.8.15-patch1
mkdir build && cd build
../configure --prefix=/home/diehl/local/hdf5-1.8.15/ --enable-parallel 
make -j 
make test
make install
cd ../..
{% endhighlight %}

## Building [NETCDF](https://www.unidata.ucar.edu/downloads/netcdf/index.jsp) (netcdf-4.3.3.1) 
{% highlight bash %}
wget https://www.unidata.ucar.edu/downloads/netcdf/ftp/netcdf-cxx4-4.3.0.tar.gz
tar -xf netcdf-cxx4-4.3.0.tar.gz
cd netcdf-cxx4-4.3.0
H5DIR=/home/diehl/local/hdf5-1.8.15/ 
export CPPFLAGS="-I${H5DIR}/include" 
export LDFLAGS=-L${H5DIR}/lib 
# Configure NetCDF 
mkdir build && cd build
../configure --prefix=/home/diehl/local/netcdf-4.3.3.1/  --disable-netcdf-4 --disable-dap --enable-parallel 
make -j
make install
cd ../..
{% endhighlight %}

## Building [Trilions](https://trilinos.org/download/) (trilinos-12.0.1)
{% highlight bash  %}
wget https://github.com/trilinos/Trilinos/archive/trilinos-release-12-0-1.tar.gz
tar -xf trilinos-release-12-0-1.tar.gz
cd trilinos-release-12-0-1
mkdir build && cd build
cmake \
-D CMAKE_INSTALL_PREFIX:PATH=/home/diehl/local/trilinos-12.0.1 \
-D CMAKE_CXX_FLAGS:STRING="-O2 -ansi -pedantic -ftrapv -Wall -Wno-long-long" \
-D CMAKE_BUILD_TYPE:STRING=RELEASE \
-D Boost_NO_SYSTEM_PATHS=ON \
-D TPL_ENABLE_MPI=ON \
-D CMAKE_CXX_COMPILER=/home/diehl/local/openmpi-2.0.1/bin/mpicxx \
-D CMAKE_C_COMPILER=/home/diehl/local/openmpi-2.0.1/bin/mpicc \
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
-D HDF5_INCLUDE_DIRS:PATH="/home/diehl/local/hdf5-1.8.15/include" \
-D HDF5_LIBRARY_DIRS:PATH="/home/diehl/local/hdf5-1.8.15/lib" \
-D TPL_ENABLE_Netcdf:BOOL=ON \
-D Netcdf_INCLUDE_DIRS:PATH="/home/diehl/local/netcdf-4.3.3.1/include" \
-D Netcdf_LIBRARY_DIRS:PATH="/home/diehl/local/netcdf-4.3.3.1/lib" \
-D TPL_ENABLE_MPI:BOOL=ON \
-D TPL_ENABLE_BLAS:BOOL=ON \
-D TPL_ENABLE_LAPACK:BOOL=ON \
-D TPL_ENABLE_Boost:BOOL=ON \
-D Boost_INCLUDE_DIRS:PATH="/home/diehl/local/boost-1-62/include" \
-D Boost_LIBRARY_DIRS:PATH="/home/diehl/local/boost-1-62/lib" \
-D CMAKE_VERBOSE_MAKEFILE:BOOL=OFF \
-D Trilinos_VERBOSE_CONFIGURE:BOOL=OFF \
-D Trilinos_ENABLE_TESTS=OFF \
..
make -j
make install
cd ../..
{% endhighlight %}

## Building [Peridigm](https://peridigm.sandia.gov/) (1.4.1) 
{% highlight bash %}
git clone https://github.com/peridigm/peridigm.git
cd peridigm
mkdir build && cd build
cmake \
-D CMAKE_BUILD_TYPE:STRING=Release \
-D Boost_NO_SYSTEM_PATHS=ON \
-D Trilinos_DIR:PATH=/data/diehl/local/trilinos-12.0.1/lib/cmake/Trilinos/ \
-D CMAKE_CXX_COMPILER=/home/diehl/local/openmpi-2.0.1/bin/mpicxx \
-D CMAKE_C_COMPILER=/home/diehl/local/openmpi-2.0.1/bin/mpicc \
-D BOOST_ROOT=/home/diehl/local/boost-1.62 \
-D CMAKE_CXX_FLAGS:STRING="-O2 -Wall -ansi -pedantic -Wno-long-long -ftrapv -Wno-deprecated -std=gnu++11 " \
..
make -j
{% endhighlight %}

## Running Peridigm
{% highlight bash %}
export LD_LIBRARY_PATH=/data/diehl/local/openmpi-2.0.1/lib/:/home/diehl/local/openmpi-2.0.1/lib/:$LD_LIBRARY_PATH
export LIBRARY_PATH=/data/diehl/local/openmpi-2.0.1/lib/:/home/diehl/local/openmpi-2.0.1/lib/:$LIBRARY_PATH
 mpiexec -np 1 ./src/Peridigm ../examples/twist_and_pull/twist_and_pull.peridigm
{% endhighlight %}

