---
layout: post
title: Using openvpn with md5 cert in Fedora 22
tags: 
  -  Fedora
---
Fedora 22 uses the package openvpn (2.3.8-1.fc22), where default of security issues the md5 algorithm for openvpn connections is not allowed. The first line enables it for this session. 
{% highlight bash  %}
$ export OPENSSL_ENABLE_MD5_VERIFY=1
$ openvpn client.ovp
{% endhighlight %}

