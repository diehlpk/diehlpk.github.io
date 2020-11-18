---
layout: post
title: Building HPX on rosam
categories: blog
tags: [Building]
author: diehlpk
---

## Login to rostam 

I assume that you followd followed the instructions and you can login to rostam.cct.lsu.edu the head ndoe of the cluster. From this node, you will compile HPX, generate the slurm 
input files, and will submit jobs.  After unsing ssh to connect rostam, you should see following output in the temrinal 


{% highlight bash %}
--> Note:
    Your work directory is /work/diehlpk

Filesystem      Size  Used Avail Use% File
-                50G   23G   28G  45% /home/diehlpk
-                  0     0     0    - /work

[diehlpk@rostam0 ~]$
{% endhighlight %}

For more details about [ssh](https://linux.die.net/man/1/ssh) we refer to this [tutorial](https://www.ssh.com/ssh/command/).

## Download HPX

First, we generate a folder Compile ([mkdir](https://linux.die.net/man/1/mkdir)) where all of the compiled libraries and HPX will be compiled. Second, we change ([cd](https://linux.die.net/man/1/cd)) to the folder. Third, we download the latest stable HPX library using [wget](https://linux.die.net/man/1/wget) command. Forth, we use the [tar](https://linux.die.net/man/1/ssh) command to unpack the archive. 


{% highlight bash %}
mkdir Compile
cd Compile
wget https://github.com/STEllAR-GROUP/hpx/archive/stable.tar.gz
tar -xf stable.tar.gz
{% endhighlight %}

Note if you have any issues with the latest version or need some recent added features you can compile the master branch from Github 

{% highlight bash %}
mkdir Compile
cd Compile
git clone https://github.com/STEllAR-GROUP/hpx.git
{% endhighlight %}


https://github.com/STEllAR-GROUP/hpx.git

## Compile HPX

### Check for the default modules

On most clusters the [module](https://linux.die.net/man/1/module) command is used to manage different compilers and libaries. On rostam default modules are
loaded which are the versions of compilers and libraries, we know HPX compiles with. We run the command 

{% highlight bash %}
module list
{% endhighlight %}

and we will see all default loaded modules

{% highlight bash %}
Currently Loaded Modules:
  1) gcc/10.2.0             3) papi/6.0.0   5) python/3.8.2   7) ucx/1.8.1    9) hwloc/2.2.0
  2) boost/1.73.0-release   4) git/2.25.1   6) cmake/3.16.4   8) pmix/3.1.5  10) Rostam2
{% endhighlight %}

### Load openmpi for the distributed runs

First, we check what versions of the openmpi compiler 

{% highlight bash %}
module avail openmpi
{% endhighlight %}

are available 

{% highlight bash %}
---------------------------- /opt/apps/gcc10/modulefiles -------
   openmpi/3.1.6    openmpi/4.0.5 (L,D)
{% endhighlight %}

and we decide to load the latest version

{% highlight bash %}
module load openmpi/4.0.5
{% endhighlight %}

### Configuration 

We call [cmake](https://linux.die.net/man/1/cmake) to configure HPX. Note that we have to add -DHPX_WITH_PARCELPORT_MPI=ON since we want to use the MPI parcelport.

{% highlight bash %}
cd hpx-stable
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Release -DHPX_WITH_PARCELPORT_MPI=ON .. 
{% endhighlight %}

### Compilation

Now, we compile hPX using the [make](https://linux.die.net/man/1/make) command

{% highlight bash %}
make -j 8
{% endhighlight %}

This will take a while and you can go and crap some coffee. Hopefully, HPX will be compiled when you return.

## Preparing the slurm files





