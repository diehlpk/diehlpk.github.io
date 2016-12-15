---
layout: post
title: Building Peridigm 1.4.1 on Ubuntu 12.04
tags:
  - Building
---

<h1>Prerequierements</h1>
<ul>
<li> <a href="http://www.boost.org/">Boost</a> with OpenMPI support >= 1.55.0 </li>
<li> zlib >= 1.2.3 (Ubuntu package)</li>
<li> curl >= 7.18.0 (Ubuntu package)</li>
<li> g++  >= 4.9 </li>
</ul>

<h1>Building <a href="https://www.hdfgroup.org/downloads/index.html">HDF5</a> (hdf5-1.8.15-patch1)</h1>
{% highlight bash %}
#set environment variables for MPI compilers
export CC=mpicc 
export CXX=mpicxx 
export FC=mpif90 
export F77=mpif77 
# Configure HDF5 
../configure --prefix=/home/diehl/local/hdf5-1.8.15/ --enable-parallel 
make -j 
make test
make install
{% endhighlight %}

<h1>Building <a href="https://www.unidata.ucar.edu/downloads/netcdf/index.jsp">NetCDF</a> (netcdf-4.3.3.1) </h1>
{% highlight bash %}
# Set environment variables for MPI compilers
export CC=mpicc 
export CXX=mpicxx 
export FC=mpif90 
export F77=mpif77 
# Modify the following #define statements in the netcdf.h.
#define NC_MAX_DIMS 65536
#define NC_MAX_ATTRS 8192
#define NC_MAX_VARS 524288
#define NC_MAX_NAME 256
#define NC_MAX_VAR_DIMS 8
H5DIR=/home/diehl/local/hdf5-1.8.15/ 
export CPPFLAGS="-I${H5DIR}/include" 
export LDFLAGS=-L${H5DIR}/lib 
# Configure NetCDF 
CPPFLAGS="-I${H5DIR}/include" LDFLAGS=-L${H5DIR}/lib  ../configure --prefix=/home/diehl/local/netcdf-4.3.3.1/  --disable-netcdf-4 --disable-dap --enable-parallel 
make -j
make install
{% endhighlight %}

<h1>Building <a href="https://trilinos.org/download/">Trilinos</a> (trilinos-12.0.1)</h1>
{% highlight bash  %}
cmake \
-D CMAKE_INSTALL_PREFIX:PATH=/home/diehl/local/trilinos-12.0.1 \
-D CMAKE_CXX_FLAGS:STRING="-O2 -ansi -pedantic -ftrapv -Wall -Wno-long-long" \
-D CMAKE_BUILD_TYPE:STRING=RELEASE \
-D Boost_NO_SYSTEM_PATHS=ON \
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
-D Boost_INCLUDE_DIRS:PATH=/opt/packages/boost-1.55.0-gcc-4.9-openmpi-1.7.5-gcc-4.9/include \
-D Boost_LIBRARY_DIRS:PATH=/opt/packages/boost-1.55.0-gcc-4.9-openmpi-1.7.5-gcc-4.9/lib \
-D CMAKE_VERBOSE_MAKEFILE:BOOL=OFF \
-D Trilinos_VERBOSE_CONFIGURE:BOOL=OFF \
..
make -j
make install
{% endhighlight %}

<h1>Building <a href="https://peridigm.sandia.gov/">Peridigm</a> (1.4.1) </h1>
{% highlight bash %}
cmake \
-D CMAKE_BUILD_TYPE:STRING=Release \
-D Boost_NO_SYSTEM_PATHS=ON \
-D Trilinos_DIR:PATH=/home/diehl/local/trilinos-12.0.1/lib/cmake/Trilinos/ \
-D CMAKE_C_COMPILER:STRING=/opt/packages/openmpi-1.7.5-gcc-4.9/bin/mpicc \
-D CMAKE_CXX_COMPILER:STRING=/opt/packages/openmpi-1.7.5-gcc-4.9/bin/mpicxx \
-D BOOST_ROOT=/opt/packages/boost-1.55.0-gcc-4.9-openmpi-1.7.5-gcc-4.9/ \
-D CMAKE_CXX_FLAGS:STRING="-O2 -Wall -ansi -pedantic -Wno-long-long -ftrapv -Wno-deprecated -std=gnu++11" \
..
{% endhighlight %}

