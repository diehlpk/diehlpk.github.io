---
layout: post
title: Building HPX on rostam
categories: blog
tags: [Building]
author: diehlpk
---

## Login to rostam 

I assume that you followed followed the instructions and you can login to rostam.cct.lsu.edu the head node of the cluster. From this node, you will compile HPX, generate the slurm 
input files, and will submit jobs.  After using ssh to connect rostam, you should see following output in the terminal 


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

On most clusters the [module](https://linux.die.net/man/1/module) command is used to manage different compilers and libraries. On rostam default modules are
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

Note that we have a bug with the gcc/10.2.0 compiler and therefore we change the compiler

{% highlight bash %}
module unload gcc/10.2.0
module load gcc/8.3.1s
module unload boost/1.73.0-release
module load boost/1.69.0-release
{% endhighlight %}

Note that we have to load a different boost version which was compiled with the same compiler.

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

### Shared memory

For the shared memory run, we create a file hpx-shared.sbatch with the content below

{% highlight bash %}
#!/usr/bin/env bash

#SBATCH -o hostname_%j.out
#SBATCH -t 00:10:00
#SBATCH -p marvin
#SBATCH -N 1
#SBATCH -D /home/diehlpk/Compile/hpx-stable/build/bin
module load gcc/8.3.1s
module load boost/1.69.0-release
srun 1d_stencil_4 --np=12 --nd=5 --nx=100 
{% endhighlight %}

Note that --np specifies the number of partitions, --nd specifies the depth of the semaphore, and --nx specifies the amount of nodes per partition. 

To submit the file, we use following command

{% highlight bash %}
[diehlpk@rostam0 ~]$ sbatch benchmarkHPX.sbatch 
Submitted batch job 24924
{% endhighlight %}

With the following command, we can list our current jobs

{% highlight bash %}
[diehlpk@rostam0 ~]$ squeue -u diehlpk
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON) 
             24740    medusa simulate  diehlpk  R 2-04:29:55      1 medusa01 
             24741    medusa simulate  diehlpk  R 2-04:29:55      1 medusa02 
             24742    medusa simulate  diehlpk  R 2-04:29:55      1 medusa03 
{% endhighlight %}

Once the simulation finished, we can list the content of the output file using the [cat](https://linux.die.net/man/1/cat) command

{% highlight bash %}
[diehlpk@rostam0 ~]$ cat Compile/hpx-stable/build/bin/hostname_24924.out 

  Local host: marvin01
--------------------------------------------------------------------------
OS_Threads,Execution_Time_sec,Points_per_Partition,Partitions,Time_Steps
16,                   0.004866721, 100,                  12,                   45     
{% endhighlight %}

to obtain the results of our run. 

Please play around with the three options and look into the performance of the application. 

### Distributed memory 

We copy the file hpx-shared.sbatch to hpx-distributed.sh and change it to 


{% highlight bash %}
#!/usr/bin/env bash

#SBATCH -o hostname_%j.out
#SBATCH -t 00:10:00
#SBATCH -p marvin
#SBATCH -N 1
#SBATCH -D /home/diehlpk/Compile/hpx-stable/build/bin
module load gcc/8.3.1s
module load boost/1.69.0-release
srun 1d_stencil_8 --np=12 --nd=5 --nx=100 
{% endhighlight %}

Note that you now can change the parameter #SBATCH -N to specify the amount of nodes. 




