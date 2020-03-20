---
layout: post
title: Google Summer of Code projects
categories: blog
tags: [Coding]
author: diehlpk
---
Here is a list of all the Google Summer of Code projects I mentored.

## HPX Backend for [OpenCV](https://opencv.org/) (2018)

This project is co-mentored by Mikael Simberg and John Biddiscombe and is done by [Jakub Golinowski](https://www.linkedin.com/in/jakub-golinowski).

### Project description

The Image processing toolbox OpenCV supports multithreading in multiple ways, i.a. via TBB or OpenMP, but not with the use of HPX. Therefore, OpenCV should be equipped with reliable HPX support for parallelism. In this way both the performance of the OpenCV and the reach of HPX will be increased.

--- 

## Alternative smart executors (2018)

This project is co-mentored by Marcin Copik and Zahra Khatami and is done by Gabriel Laberge.

### Project description

HPX allows users to parallel their for-loops. The user can change values of chunk size and prefetching distance with existing execution policies. Some of these policies use machine learning the optimal chunk size and prefetching distance for a given for-loop. However, these machine learning algorithms are classification algorithms so the number of possible outcome is limited. The idea is to use regression algorithms to allow for as many outcomes as needed.

Reference:

* G. Laberge, S. Shirzad, P. Diehl, H. Kaiser, S. Prudhomme and A. S. Lemoine, "Scheduling Optimization of Parallel Linear Algebra Algorithms Using Supervised Learning," 2019 IEEE/ACM Workshop on Machine Learning in High Performance Computing Environments (MLHPC), Denver, CO, USA, 2019, pp. 31-43.

--- 

## [HPXCL](https://github.com/STEllAR-GROUP/hpxcl) – Asynchronous Integration of CUDA and OpenCL to [HPX](https://github.com/STEllAR-GROUP/hpx) (2017)

The project [HPXCL](https://github.com/STEllAR-GROUP/hpxcl) is done by [Madhavan Seshadri](http://madhavanseshadri.com/)

### Project description

Massively parallel applications are in the dawn of our future. The scale of problems and the amount of data available have made it infeasible to solve 
a meaningful problem in a single computer. As such, in such a scale, it is imperative to combine CPUs and accelerator cards such as GPUs to achieve one 
unified computing source. HPXCL aims at unifying kernel launch and data transfer into HPX asynchronous graph through seamless integration. 
However, the current implementation of the system with CUDA fails to achieve the desired performance improvement metrics while running in a cluster 
of computers. The proposal is aimed at improving the performance of CUDA-based HPXCL applications through an ‘Event’ triggered mechanism. 
Appropriate tests are also to be written to ensure necessary functionality performs as required. 
Standard benchmarking algorithms (Floyd Warshall, FFT etc.) will also be implemented in HPXCL, OpenCL and CUDA to validate, 
measure and improve the performance of the existing system, while also keeping in mind the new functionality added.

Blog posts:

* [Benchmarks Accelerator Devices](https://madhavan001.github.io/Benchmarks-accelerator-devices/)
* [GSoC Final Evaluation](https://madhavan001.github.io/GSoC-Final-Evaluation/)

Reference:

* P. Diehl, M. Seshadri, T. Heller and H. Kaiser, "Integration of CUDA Processing within the C++ Library for Parallelism and Concurrency (HPX)," 2018 IEEE/ACM 4th International Workshop on Extreme Scale Programming Models and Middleware (ESPM2), Dallas, TX, USA, 2018, pp. 19-28.

--- 

## Implement a Map/Reduce Framework (2016)

[Map/Reduce](http://en.wikipedia.org/wiki/MapReduce) frameworks are getting more and more popular for big data processing (for example [Hadoop](http://hadoop.apache.org/)). By utilizing the unified and standards conforming API of the HPX run time system, we believe to be able to perfectly represent the Map/Reduce programming model. Many applications would benefit from direct support in HPX. This might include adding [Hypertable](http://hypertable.com) or similar libraries to the mix to handle the large data sets Map/Reduce is usually used with.

The project [hpxflow](https://github.com/STEllAR-GROUP/hpxflow) was successfully done by [Aalekh Nigam](https://twitter.com/_aalekh).

Blog Posts:

* [Various study over existing Parallel Processing based Framework](http://aalekhnigam.tumblr.com/post/144510275317/various-study-over-existing-parallel-processing)
* [Using Fluent Interface for hpxflow API design](http://aalekhnigam.tumblr.com/post/149356061927/using-fluent-interface-for-hpxflow-api-design)
* [Using Multiconsumer-Multiproducer Model for windowing](http://aalekhnigam.tumblr.com/post/149355148447/using-multiconsumer-multiproducer-model-for)
* [Summing up my GSoC with Stellar Group](http://aalekhnigam.tumblr.com/post/149361127187/summing-up-my-gsoc-with-ste-ar-group)

---
