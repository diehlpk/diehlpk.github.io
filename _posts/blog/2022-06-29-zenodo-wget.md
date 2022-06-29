---
layout: post
title: Download Zenodo archives using wget
categories: blog
tags: [HPC]
author: diehlpk
---

Sometimes downloading a archive from [Zendo](https://zenodo.org/) directly to a cluster comes in handy. However, Zenodo hides the direct download and using `wget` does not work. One can use the Zenodo API to receive the download URL for the archive by running  

{% highlight bash %}
curl  https://zenodo.org/api/records/5213015
{% endhighlight %}

where the last digits are the ID of the Zenodo record. In the curl output there is one entry 

{% highlight bash %}
links":{"self":"https://zenodo.org/api/files/273e913a-e11d-46e1-96dc-a28497c49d36/data.tar.gz"}
{% endhighlight %}

containing the URL to download the file directly by running

{% highlight bash %}
wget https://zenodo.org/api/files/273e913a-e11d-46e1-96dc-a28497c49d36/data.tar.gz
{% endhighlight %}

