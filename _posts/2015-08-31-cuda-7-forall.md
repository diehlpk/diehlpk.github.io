---
layout: post
title: Parallel for loop in Cuda 7.0
tags:
  - Coding
---
With the release of <a href="http://devblogs.nvidia.com/parallelforall/cuda-7-release-candidate-feature-overview/"> Cuda 7.0</a> CP++11 features are available inside of Cuda kernels. Before that feature implementing a for loop in a kernel was very confusing.
{% highlight cpp %}
__global__ void sum(int* array , int n, int* count){ \
 for (int i = blockDim.x * blockIdx.x + threadIdx.x;\
         i < n;\
         i += gridDim.x * blockDim.x)\
    {\
        atomicAdd(&(count[0]), array[i]);\
    }\
}\
{% endhighlight %} 
With the new C++11 features the for loop can be rewritten as
{% highlight cpp %}
__global__ void sum(int* array,int n , int* count){
for (auto i : grid_stride_range(0,n))
        atomicAdd(&(count[0]), array[i]);
{% endhighlight %}
For the run time of both for loops, wee see that there is nearly difference and we got the more readable code for free.<p>
<div align="center">
<img src="{{ site.url }}/assets/2015-09-1-runtime-cuda.png"style="width:604px;height:456px;">
</div>

Links:
<ul>
	<li><a href="https://github.com/harrism/cpp11-range">Range-based for loops</a></li>
	<li>[Files]({{ site.url }}/assets/2015-08-foreach.tar.gz)</li>
</ul>
