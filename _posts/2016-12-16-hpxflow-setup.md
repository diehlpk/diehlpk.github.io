---
layout: post
title: Installing HPXFLOW on Fedora 25
tags:
- Building
---
HpxFlow is a unified Batch and Stream Processing framework, over [HPX](https://github.com/STEllAR-GROUP/hpx), partially based on [Google's DataFlow Model](http://www.vldb.org/pvldb/vol8/p1792-Akidau.pdf).

# Installation and configureation of mariadb

## Installation (Server)
Install the mariadb server
{% highlight bash  %}
sudo dnf install mariadb-server 
{% endhighlight %}
Start the mariadb server serive once
{% highlight bash  %}
systemctl start mariadb.service
{% endhighlight %}
Optinal: Enable the start of the service on every boot of the system
{% highlight bash  %}
/usr/bin/mysql_secure_installation
{% endhighlight %}

## Configuration
Create a database, a user, and a table to run the [map and reduce](https://github.com/STEllAR-GROUP/hpxflow/tree/master/examples/mapreduce.cpp) example. 
{% highlight bash  %}
mysql -u root -p
MariaDB [(none)]> CREATE DATABASE test;
MariaDB [(none)]> CREATE USER 'testuser'@'localhost' IDENTIFIED BY 'yourpassword';
MariaDB [(none)]> GRANT ALL ON test.* TO 'testuser'@'localhost';
MariaDB [(none)]> FLUSH PRIVILEGES;
MariaDB [(none)]> USE test;
MariaDB [(none)]> CREATE TABLE test (one VARCHAR(20), two VARCHAR(20), three VARCHAR(20), four VARCHAR(20), five VARCHAR(20));
{% endhighlight %}

## Installation (Client)

Download the Connector [here](http://dev.mysql.com/downloads/connector/cpp/) and install the packages

{% highlight bash  %}
sudo rpm -i mysql-connector-c++-1.1.7-linux-glic2.5-x86-32bit.rpm
sudo dnf install mysql-connector-c++
{% endhighlight %}

# Installation of hpxflow

## Prerequisites

* [HPX](https://github.com/STEllAR-GROUP/hpx) -- For installation intrusctions for Fedora 25 see [here](http://diehlpk.github.io/2015/08/04/hpx-fedora.html) 

## Compile hpxflow

{% highlight bash  %}
git clone https://github.com/STEllAR-GROUP/hpxflow.git
cd hpxflow
mkdir build && cd build
cmake -DHPX_DIR=pathToHpx/build/lib/cmake/HPX ..
{% endhighlight %}

# Run the map and reduce example

{% highlight bash  %}
./examples/example_mapreduce
{% endhighlight %}
