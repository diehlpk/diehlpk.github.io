---
layout: post
title: CMake and boost
tags: 
  - CMake
  - Boost
---
Using [FindBoost](http://www.cmake.org/cmake/help/v3.0/module/FindBoost.html) from CMake and setting Boost_INCLUDE_DIRS and Boost_LIBRARY_DIRS to non systems paths often causes that CMake use the boost version found in the system paths and ignore the set paths. To force CMake using the set paths use
{% highlight bash  %}
cmake 
- D Boost_NO_BOOST_CMAKE=TRUE 
- D BOOST_ROOT:PATHNAME=<localPath>
{% endhighlight %}

