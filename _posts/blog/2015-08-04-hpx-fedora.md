---
layout: post
title: Installing HPX on Fedora 22/23/24/25
categories: blog
tags: [Building]
---
Prerequisites
=====
Install all packages for minimal installation
{% highlight bash %}
sudo dnf install gcc-c++ cmake boost-build boost boost-devel hwloc-devel hwloc gcc-gfortran papi-devel gperftools-devel docbook-dtds docbook-style-xsl libsodium-devel doxygen boost-doc fop boost-devel git
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
Add the library path of HPX to ldconfig
{% highlight bash  %}
sudo echo /opt/hpx/lib > /etc/ld.so.conf.d/hpx.conf  
sudo ldconfig
{% endhighlight %}
<p>
Links
<ul>
	<li> <a href="{{ site.url }}/assets/2015-08-hpx-dockerfile">Dockerfile</a> </li>
</ul>
