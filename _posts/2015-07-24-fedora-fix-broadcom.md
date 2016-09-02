---
layout: post
title: Fix broken broadcom-wl driver on Fedora 22
tags:
  -  Fedora
---
Fedora supports a very new linux kernel version, but mostly the Broadcom 802.11 STA driver (broadcom-wl) is mostly not compatible with this kernel version (>4.0.4). To fix this issue try to run following commands as root user. 
{% highlight bash  %}
su
# akmods --force
# modprobe wl
{% endhighlight %}
This commands checks if kmods exists for your used kernel and builds and installs wl-kmod.Thus, I was able to use the WiFi with the kernel version 4.0.8 at Fedora 22.

