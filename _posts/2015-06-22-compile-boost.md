---
layout: post
title: Building boost with OpenMPI support
---
Compliling [Boost](http://www.boost.org/) with OpenMPI support needs a lot of prerequirements in the build process. Here is a shell script for installing boost with openmpi support into any local path.
{% highlight js %}
#!/bin/bash

if [ $# != 2 ]; then \
	echo "./boostPUM VERSION INSTALL_DIR" \
	echo "./boostPUM 1_53_0 /home/diehlpk > installs boost 1_53_0 with mpi support in /home/diehlpk" \
else \
	Version="$1" \
	echo Unpacking boost \
	tar -xvf boost_$1.tar.gz \
        cd boost_$1 \
	echo Adding MPI to configuration file \
	echo "using mpi ;" >> tools/build/v2/user-config.jam \
	cp tools/build/v2/user-config.jam $HOME \
	echo Configuring boost \
 	./bootstrap.sh --prefix=$2 \
	./bjam --with-mpi \
	echo Compiling boost \
	./b2 \	
	echo Installing boost \
	./b2 --layout=tagged install \	
fi 
{% endhighlight %}
