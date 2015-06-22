---
layout: post
title: Bulding Peridigm 1.4.1 on Ubuntu 12.04
---

<h5>Prerequierements</h5>
<ul>
<li> [Boost](http://www.boost.org/) with OpenMPI support >= 1.55.0 </li>
<li> zlib >= 1.2.3 (Ubuntu package)</li>
<li> curl >= 7.18.0 (Ubuntu package)</li> 
</ul>

<h5>Building [HDF5](https://www.hdfgroup.org/downloads/index.html) (hdf5-1.8.15-patch1)  </h5>
{% highlight bash %}
#set environment variables for MPI compilers
export CC=mpicc \
export CXX=mpicxx \
export FC=mpif90 \
export F77=mpif77 \
# Configure HDF5 \
../configure --prefix=/home/diehl/local/hdf5-1.8.15/ --enable-parallel 
{% endhighlight %}

<h5>Building [NetCDF](https://www.unidata.ucar.edu/downloads/netcdf/index.jsp) </h5>

<h5>Building [Trilinos](https://trilinos.org/download/) </h5>

<h5> Building [Peridigm](https://peridigm.sandia.gov/) </h5>


