---
layout: post
title: Setup Windows for CUDA
---
Recently one researcher used my CUDA-based neighbor search lib the first
time on a Windows machine (Windows Server 2012). He wrote me that all of
the provided examples fail with this error message  
{% highlight bash  %}
" the launch timed out and was terminated. ".
{% endhighlight %}

Using CUDA on a Windows machine with one GPU for displaying and computing,
restricts the run time of a cuda kernel to a short period. I think they do 
not want that the window manager freezes. To overcome this issue for running
long kernels edit the Windows registry
{% highlight bash  %}
KeyPath   : HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers
KeyValue  : TdrLevel
ValueType : REG_DWORD
ValueData : TdrLevelOff (0) - Detection disabled 
{% endhighlight %}
For more details look <a href="https://msdn.microsoft.com/en-us/library/windows/hardware/ff569918(v=vs.85).aspx">here</a>.
