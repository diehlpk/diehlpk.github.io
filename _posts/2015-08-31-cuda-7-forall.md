---
layout: post
title: Parallel for loop in Cuda 7.0
tags:
  - Coding
---
With the release of <a href="http://devblogs.nvidia.com/parallelforall/cuda-7-release-candidate-feature-overview/"> Cuda 7.0</a> a subset of CP++11 features are available inside of Cuda kernels. These features are
<p><p>
<ul>
	<li><a href="http://en.cppreference.com/w/cpp/language/auto">Auto specifier</a></li>
	<li><a href="http://en.cppreference.com/w/cpp/language/lambda">Lambda functions</a></li>
	<li><a href="http://en.cppreference.com/w/cpp/language/range-for">Range-based for loops</a></li>
</ul>
Without these features a for loop inside a kernel looked very confusing, because the user had to deal
with the grid size and the block size to access an element of the data array on the device.
{% highlight cpp %}
__global__ void sum(int* array , int n, int* count){ 
 for (int i = blockDim.x * blockIdx.x + threadIdx.x;
         i < n;
         i += gridDim.x * blockDim.x)
    {
        atomicAdd(&(count[0]), array[i]);
    }
}
{% endhighlight %} 
With the auto specifier and the range-based for loops the kernel can be rewritten more readable and shorter.
Here we need some additional functionality [1] to iterate over the data array, because it is not possible to use the
thrust_device_vector inside the kernel and use its iterator. The get_stride_range(0,n) function returns a iterator from
0 to N to iterate over the data array without dealing with the grid size and block size. 
{% highlight cpp %}
__global__ void sum(int* array,int n , int* count){
for (auto i : grid_stride_range(0,n))
        atomicAdd(&(count[0]), array[i]);
{% endhighlight %}
For the run time of both for loops, wee see that there is nearly no difference for the computational cost per array item.
Thus, the generation and usage of the iterator does not affect the overall computational cost.
<p>
<div align="center">
<img src="{{ site.url }}/assets/2015-09-1-runtime-cuda.png" style="width:604px;height:456px;">
</div>

Links:
<ol>
	<li><a href="https://github.com/harrism/cpp11-range">Range-based for loops</a></li>
	<li><a href="{{ site.url }}/assets/2015-08-foreach.tar.gz" >Files</a></li>
</ol>
