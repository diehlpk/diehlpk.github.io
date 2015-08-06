---
layout: post
title: Installing HPX on Fedora 22
tags:
- Building
---
Prerequisites
=====
Install all package for minimal installation
{% highlight bash %}
sudo dnf install cmake boost-build boost boost-devel hwloc-devel hwloc gcc-gfortran papi-devel gperftools-devel docbook-dtds docbook-style-xsl libsodium-devel doxygen boost-doc hdf5-devel fop boost-devel boost-openmpi-devel boost-mpich-devel 
{% endhighlight %}

Building HPX
=====
Get the development branch
{% highlight bash  %}
git clone https://github.com/STEllAR-GROUP/hpx.git
{% endhighlight %}
Configure it with CMake
{% highlight bash  %}
module load mpi/mpich-x86_64
cd hpx
mkdir build
cd build
cmake -DCMAKE_INSTALL_PREFIX=/opt/hpx ..
make -j 3
make install
{% endhighlight %}
For building with examples run 
{% highlight bash  %}
cmake -DHPX_BUILD_EXAMPLES=On ..
make -j 3 examples
make install
{% endhighlight %}
Add the library path of HPX to ldconfig
{% highlight bash  %}
sudo echo /opt/hpx/lib > /etc/ld.so.conf.d/hpx.conf  
sudo ldconfig
{% endhighlight %}
