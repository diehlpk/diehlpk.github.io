---
layout: post
title: Installing HPX on Fedora 22--29
categories: blog
tags: [Building]
author: diehlpk
---

## Installation with dnf
Since Fedora 28, there is an offical package for hpx compiled with gcc, openmpi, and mpich available in the updates-testing repo.

{% highlight bash %}
dnf search hpx 
Last metadata expiration check: 1:11:50 ago on Wed 21 Nov 2018 03:02:33 PM EST.
========================== Name Exactly Matched: hpx ===========================
hpx.i686 : General Purpose C++ Runtime System
hpx.x86_64 : General Purpose C++ Runtime System
========================= Name & Summary Matched: hpx ==========================
hpx-examples.x86_64 : HPX examples
hpx-mpich.x86_64 : HPX MPICH libraries
hpx-openmpi.x86_64 : HPX Open MPI libraries
hpx-mpich-examples.x86_64 : HPX MPICH examples
hpx-openmpi-examples.x86_64 : HPX Open MPI examples
hpx-devel.i686 : Development headers and libraries for hpx
hpx-devel.x86_64 : Development headers and libraries for hpx
hpx-mpich-devel.i686 : Development headers and libraries for hpx
hpx-mpich-devel.x86_64 : Development headers and libraries for hpx
hpx-openmpi-devel.i686 : Development headers and libraries for hpx
hpx-openmpi-devel.x86_64 : Development headers and libraries for hpx
{% endhighlight %}

## Compilation

Prerequisites
=====
Install all packages for minimal installation
{% highlight bash %}
sudo dnf install gcc-c++ cmake boost-build boost boost-devel hwloc-devel hwloc gcc-gfortran papi-devel gperftools-devel docbook-dtds docbook-style-xsl libsodium-devel doxygen boost-doc fop git
{% endhighlight %}

Building HPX
=====
Get the development branch of <a href="http://stellar.cct.lsu.edu/tag/hpx/">HPX</a>
{% highlight bash  %}
git clone https://github.com/STEllAR-GROUP/hpx.git
{% endhighlight %}
Configure it with CMake
{% highlight bash  %}
cd hpx
mkdir build
cd build
cmake -DCMAKE_INSTALL_PREFIX=/opt/hpx ..
make -j 
make install
{% endhighlight %}
For not building the examples run 
{% highlight bash  %}
cmake -DCMAKE_INSTALL_PREFIX=/opt/hpx -DHPX_BUILD_EXAMPLES=Off ..
make -j 
make install
{% endhighlight %}
Add the library path of HPX to ldconfig. Note you have to change the path depending on 32bit or 64bit
{% highlight bash  %}
sudo echo /opt/hpx/lib > /etc/ld.so.conf.d/hpx.conf  
sudo ldconfig
{% endhighlight %}
<p>
Links
<ul>
	<li> <a href="{{ site.url }}/assets/2015-08-hpx-dockerfile">Dockerfile</a> </li>
</ul>
