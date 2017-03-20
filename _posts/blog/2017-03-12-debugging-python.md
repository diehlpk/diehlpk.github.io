---
layout: post
title: Debugging your python code
categories: blog
tags: [Coding]
author: diehlpk
---


## Profiler

A profiler is helpful to analyze your code, when your code is slow in general or got slower after some changes. To profile your code and get the information how long it took to execute one line and how often this line was executed you can use a tool called [line_profiler](https://pypi.python.org/pypi/line_profiler/). For installing the tool use 

```bash
$ pip install --user line_profiler
```
For example to investigate how long the execution of one line takes and how often a line is executed the `@profile` is add to the function of interest.

```python
@profile
def ackermann(m,n):

    if m == 1:
        return n + 1
    if m > 0 and n == 0:
        return ackermann(m-1,1)
    if m > 0 and n > 0:
        return ackermann(m-1,ackermann(m,n-1))
                 
print ackermann(3,2)
```
Now mention the code above is saved in the file `ackermann.py` and we can execute on Linux and Mac OS X

```bash
$ kernprof -l -v ackermann.py 
```

and on Windows

```bash
$ kernprof.exe -l -v ackermann.py 
```

which yields

```bash
13
Wrote profile results to ackermann.py.lprof
Timer unit: 1e-06 s

Total time: 0.000195 s
File: ackermann.py
Function: ackermann at line 1

Line #      Hits         Time  Per Hit   % Time  Line Contents
==============================================================
     1                                           @profile
     2                                           def ackermann(m,n):
     3                                           
     4        90           42      0.5     21.5      if m == 1:
     5        42           26      0.6     13.3          return n + 1
     6        48           23      0.5     11.8      if m > 0 and n == 0:
     7         7           15      2.1      7.7          return ackermann(m-1,1)
     8        41           23      0.6     11.8      if m > 0 and n > 0:
     9        41           66      1.6     33.8          return ackermann(m-1,ackermann(m,n-1))
```
Here, we see e.g. that line 4 was called 90 times and all calls cost 42 time units which is 0.5 time units for one call and this is 21.5% of the overall computation time of the code. With this information we can investigate where our code is slow and identify the bottleneck and may improve it there, if possible.
