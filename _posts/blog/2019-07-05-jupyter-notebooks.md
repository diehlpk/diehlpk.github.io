---
layout: post
title: Using Jupyter notebooks for assignments
categories: blog
tags: [Teaching]
author: diehlpk
---


### Writing a C++ program 

We will look into two different ways to write this program using the Jupyter server.

```cpp
#include <string>
#include <vector>
#include <iostream>

int main(){

std::vector<int> values = {1,2,3};

for ( auto v : values)
	std::cout << v << std::endl;

return 0;
}
```

#### Using a Jupyer notebook

![GitHub Logo]({{ site.url }}/assets/2019-06-04-jupyter-login.png)


After you logged in to the Jupyter server, click on new, and click on C++ 14.

![GitHub Logo]({{ site.url }}/assets/2019-06-04-jupyter-new.png)

Now you have your notebook having cells which contain your C++ code. Note that you have to have 
one cell containing all the includes header files, see Cell 1, and this cell can not have any
C++ code included. To compile a cell press Ctrl+Enter. 

![GitHub Logo]({{ site.url }}/assets/2019-06-04-jupyter-notebook-cpp.png)


#### Using the [vim](https://www.vim.org/) editor
 
After you logged in to the Jupyter server, click on new, and click on Terminal.

![GitHub Logo]({{ site.url }}/assets/2019-06-04-jupyter-new.png)

Now, you can type vim easy.cpp in the terminal to open the file easy.cpp. 

![GitHub Logo]({{ site.url }}/assets/2019-06-04-jupyter-vim.png)

For the basic usage of vim, I recommend to use this interactive [tutorial](https://www.openvim.com/). To close the editor
you would need to type :q. 


![GitHub Logo]({{ site.url }}/assets/2019-06-04-jupyter-terminal-compile.png)

Now you can compile your program and execute it in the terminal.



### Setup github

You need to configure github once and later you can clone and add new files to your repo. You can either add a cpp file or a jupyter notebook 
for each of your assignments. Just use the following naming scheme: exercise1-2.cpp where the first number indicates the exercise sheet and the second
number the exercise. 

![GitHub Logo]({{ site.url }}/assets/2019-06-04-jupyter-github.png)

Note that you will get diffferent url for your assignments. Please find more details [here](https://www.diehlpk.de/blog/githubclassroom/).

### Video tutorial 

[![Alt text](https://img.youtube.com/vi/frFVguK-dWE/0.jpg)](https://www.youtube.com/watch?v=frFVguK-dWE)






