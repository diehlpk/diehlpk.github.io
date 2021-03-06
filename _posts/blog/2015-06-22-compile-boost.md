---
layout: post
title: Building boost with OpenMPI support
categories: blog
tags: [Building]
author: diehlpk
---
Compiling [Boost](http://www.boost.org/) with OpenMPI support needs a lot of requirements in the build process. Here is a shell script for installing boost with OpenMPI support into any local path.
{% highlight bash %}
#!/bin/bash 
if [ $# != 2 ]; then 
	echo "./boostPUM VERSION INSTALL_DIR" 
else 
	Version="$1" 
	echo Unpacking boost 
	tar -xvf boost_$1.tar.gz 
        cd boost_$1 
	echo Adding MPI to configuration file 
	echo "using mpi ;" >> tools/build/v2/user-config.jam 
	cp tools/build/v2/user-config.jam $HOME 
	echo Configuring boost 
 	./bootstrap.sh --prefix=$2 
	./bjam --with-mpi 
	echo Compiling boost 
	./b2 	
	echo Installing boost 
	./b2 --layout=tagged install 	
fi 
{% endhighlight %}
