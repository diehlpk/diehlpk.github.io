---
layout: post
title: Advanced Parallel Programming in C++
categories: blog
tags: [C++,HPX]
author: diehlpk
---
<script type="text/x-mathjax-config">
    MathJax.Hub.Config({
      tex2jax: {
        skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
        inlineMath: [['$','$']]
      }
    });
  </script>
  <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

Many applied mathematics codes are based on the C++ programming language. However, many of these codes do not utilize modern C++ features, especially the features from the recent C++ 17 standard for parallel computations. These features can significantly simplify parallel computations using multiple cores. This review briefly introduces asynchronous programming facilities introduced in the C++ 11 standard and the parallel algorithms introduced in the C++ 17 standard. With these two paradigms, C++ code can be accelerated using multiple cores using the C++ standard without any need for some external special purpose libraries, like e.g. OpenMP. The C++20 standard made additional and valuable contributions to the C++ api for parallelism and concurrency. While these may still be unavailable in some compilers, they are already implemented in HPX [4].

## Asynchronous programming

The C++11 standard [7] has introduced asynchronous task programming. Here, the concept of futurization using `std::future` was introduced. A future is a placeholder for the result of an asynchronous function (launched e.g. using `std::async()`). The runtime promises that once the computation of the task passed to `std::async()` has finished, the future will receive the result. One can use the function `.get()` to access the result. If the computation has finished the result will be returned. If the computation is still ongoing, the function will suspend the current thread until the future has become ready, at which point the result is returned to the user. Let us look at the following Taylor expansion for the natural logarithm

$$ \ln(x) = \sum\limits_{n=1}^N \frac{(-1)^{n+1}}{n}(x-1)^n \textbf{.} $$

Listing 1  shows the asynchronous computation of the Taylor series. First, a function `taylor_part` that computes a part of the sum is defined in Line 5. In Line 20 the sum of length $n$ is separated into two partitions of $\frac{n}{2}$ and each of them is asynchronously launched, and a future is returned. Since these two function launches run concurrently on two cores, we need to synchronize their execution and collect the results. In Line 25 the `.get()}` function is called to access the result of each of the futures. Note that the code will introduce a barrier and waits until the first and second future are ready.

![Listing1!]({{ site.url }}/assets/2021-10-28-listing1.svg "Example to for asyncrhonous programming.")

## Parallel algorithms

A common opportunity for shared-memory parallel programming in C++ is Open Multi-Processing (OpenMP) [1]. Let us look at the implementation of computing the square root of all elements in a vector $v$ of size $n$ 

$$   v_i = \sqrt{v_i}, \; \forall i \in {1,\ldots,n} $$

in a parallel fashion using OpenMP, see Listing 1. In Line 11, a `std::vector` is generated with the length $n=10000$ and in Line 13 the vector is filled with random numbers using the algorithms provided by the C++ standard library. In Line 16 a `for` loop is used to iterate over the elements of the vector. Now, the `#prgama`-based OpenMP API is used to parallize the `for` loop. In Line 15 the `#prgama` to execute the loop in parallel is added. However, an additional API is needed to achieve the shared-memory parallelism. 

![Listing3!]({{ site.url }}/assets/2021-10-28-listing3.svg "Example to compute the element-wise square root of a vector using OpenMP.")

In the latest C++ 17 standard~\cite{cxx17_standard}, the so-called parallel algorithms were introduced. The shared-memory parallelism is based on the thread building blocks (TBB)~\cite{10.5555/1352079.1352134} library. Now, it is possible to write parallel code directly using the C++ standard, and there is no need to use a second API anymore. The C++ standard library contains $69$ algorithms which work on the so-called containers, like `std::vector` or `std::list`. In C++ 17 the so-called execution policies were introduced to these $69$ algorithms to execute them in parallel. First, we will look into the previous example, see Listing 2. Up to Line 14 the code is identical, expect of the new header file `#include <execution`, which is needed for the execution policies. In Line 16 a vector containing the indices of each vector element is generated. In Line 20 the OpenMP parallel `for` loop is replaced by `std::for_each` from the C++ standard library algorithms. Note that this was possible before. However, the first argument of this function, the so-called execution policy, defines that this algorithm is executed in parallel. The C++ 17 standard introduced the following execution policies:

* **Sequential execution**: By adding `std::execution::seq` the algorithm is executed sequentially using one thread as in the previous C++ standards.
* **Parallel execution**: By adding `std::execution::par` the algorithm is executed in parallel using all available threads. 
* **Vectorized parallel execution**: By adding `std::execution::par_unseq` the algorithm is executed in parallel but in addition vectorization is used.

Now by specifying the execution policy in Line 21 the algorithm is easily parallized. Note that this happened using the C++ standard, and no external tool, like OpenMP, was needed.

![Listing4!]({{ site.url }}/assets/2021-10-28-listing4.svg "Example to compute the element-wise square root of a vector using C++.")

Second, we will look into some small example to compute the sum $s$ of all elements in a vector $v$ with $n$ elements

$$   s = \sum\limits_{i=0}^n v_i \text{,} $$

see Listing 3. In Line 3 a `std::vector` with the length `n` is generated. The first algorithm of the C++ Standard Library `std::fill` is used to fill all elements with negative one, see Line 11. And finally, the second algorithm `std::accumulate` is used to compute the sum of all elements. Note that the naive approach would be to use a `for` loop to iterate over all the elements. In Line 15 the result is printed for validation. Again, one can use the execution policies to easily parralize this code by just adding the execution policy in Line 11 and Line 13, respectively. The corresponding code is shown in Listing 4.

![Listing5!]({{ site.url }}/assets/2021-10-28-listing5.svg "Example to compute the sum of all elements in the vector using the C++ standard library")

![Listing6!]({{ site.url }}/assets/2021-10-28-listing6.svg "Example to compute the sum of all elements in the vector using the parallel algorithms provided by the C++
17 standard.")

These two small examples only showed few functions of the C++ 17 standard, which are experimentally supported by the GNU compiler collection (gcc) $\geq$ 9 and the Microsoft Visual Studio compiler (MVSC). However, the C++ standard library for parallelism and concurrency (HPX) implements many more of the defined features in the C++ 17 standard. Note that you can replace the `std::` name space by `hpx::` name space, since HPX strictly enhance the C++ 17 standard. We will show two small examples with new features which are not yet implemented in the major implementations. First, HPX provides some easier way to iterate over a vector without generating a vector of indices using `std::for_each`, see Listing 2. Listing 6 shows the simplification for iterating over the vector. In the previous example, we had to generate the vector of indices, which increases the memory consumption of the program. In Line~\ref{lst:for:each:hpx:loop}, we use a `hpx::for_loop` which is more like the `for` loop where the start index is provided as the second argument and the end index as the third argument. In the lambda function, we can access the index, $i$ which will go from zero up to `v.size()`. In addition, the parallel algorithms can be combined with the concept of futurization to obtain a `hpx::future`. Note that this is not provided by the C++ 17 standard.

![Listing7!]({{ site.url }}/assets/2021-10-28-listing7.svg "Example to compute the sum of all elements in the vector using the parallel algorithms provided by HPX.")


## Supplementary materials

The source code of all the examples is available on [GitHub](https://github.com/diehlpk/modern-cpp-examples) or Zenodo, respectively. The build system [CMake](https://cmake.org/) is used to compile all the examples.  

## Acknowledgments

I would like to acknowledge the students of the course ``Parallel Computational Math'' offered at the Mathematics Department at Louisiana State University for their feedback while teaching these modern C++ features as part of the course.

## References

1. Leonardo Dagum and Ramesh Menon. Openmp: an industry standard api for shared-memory programming. Computational Science & Engineering, IEEE, 5(1):46–55, 1998.
2. Patrick Diehl, Prashant K Jha, Hartmut Kaiser, Robert Lipton, and Martin Lévesque. An asynchronous and task-based implementation of peridynamics utilizing hpx—the c++ standard library for parallelism and concurrency. SN Applied Sciences, 2(12):1–21, 2020.
3. Prashant K Jha and Patrick Diehl. Nlmech: Implementation of finite difference/meshfree discretization of nonlocal fracture models. Journal of Open Source Software, 6(65):3020, 2021.
4. Hartmut Kaiser, Patrick Diehl, Adrian S Lemoine, Bryce Adelstein Lelbach, Parsa Amini, Agustı́n Berge, John Biddiscombe, Steven R Brandt, Nikunj Gupta, Thomas Heller, et al. HPX-the c++ standard library for parallelism and concurrency. Journal of Open Source Software, 5(53):2352, 2020.
5. Dominic C Marcello, Sagiv Shiber, Orsola De Marco, Juhan Frank, Geoffrey C Clayton, Patrick M Motl, Patrick Diehl, and Hartmut Kaiser. octo-tiger: a new, 3D hydrodynamic code for stellar mergers that uses hpx parallelization. Monthly Notices of the Royal Astronomical Society, 504(4):5345–5382, 04 2021.
6. Chuck Pheatt. Intel® threading building blocks. J. Comput. Sci. Coll., 23(4):298, April 2008.
7. The C++ Standards Committee. ISO International Standard ISO/IEC 14882:2011, Programming Language C++. Technical report, Geneva, Switzerland: International Organization for Standardization (ISO)., 2011. [http://www.open-std.org/jtc1/sc22/wg21](http://www.open-std.org/jtc1/sc22/wg21).
8. The C++ Standards Committee. ISO International Standard ISO/IEC 14882:2017, Programming Language C++. Technical report, Geneva, Switzerland: International Organization for Standardization (ISO)., 2017. [http://www.open-std.org/jtc1/sc22/wg21](The C++ Standards Committee. ISO International Standard ISO/IEC 14882:2017, Programming Language
C++. Technical report, Geneva, Switzerland: International Organization for Standardization (ISO)., 2017.
http://www.open-std.org/jtc1/sc22/wg21]
