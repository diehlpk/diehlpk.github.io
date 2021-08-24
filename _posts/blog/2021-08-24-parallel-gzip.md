---
layout: post
title: Parallel compression
categories: blog
tags: [Tools]
author: diehlpk
---

Sometimes it can be useful to compress large archives in parallel to speedup the task. A common tool on Linux is [gzip](https://linux.die.net/man/1/gzip)

{% highlight bash %}
gzip data.tar
{% endhighlight %}

to compress the data.tar archive and obtain the compressed data.tar.gz. To speedup the process there is a parallel implementation [pigz](https://zlib.net/pigz/) available. You 
can download pigz and compile it using the following code snippt

{% highlight bash %}
wget https://github.com/madler/pigz/archive/refs/tags/v2.6.tar.gz
tar -xvf v2.6.tar.gz 
cd v.2.6/
make
{% endhighlight %}

To compress the archive in parallel you can run 

{% highlight bash %}
./v.2.6/pigz -p 12 data.tar
{% endhighlight %}

where -p specifies the pthreads you want to use. In this case we will 12 pthreads to compress the archive. More options are available [here](https://zlib.net/pigz/pigz.pdf).


