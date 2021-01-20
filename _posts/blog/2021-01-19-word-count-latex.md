---
layout: post
title: Word count in LaTeX documents
categories: blog
tags: [Latex]
author: diehlpk
---

Sometimes it can be useful to count the word of a LaTex document. One option is to use [pdftotext](https://linux.die.net/man/1/pdftotext) and pipe it to the [wc](https://linux.die.net/man/1/wc) command.

{% highlight bash %}
pdftotext template.pdf - | wc -w
6910
{% endhighlight %}

However, only the total word count is printed to the terminal. Sometimes, more details are needed, e.g. the word count in the text, the wourd count of the captions, or the amount of floating environments. Here, [texcount](https://app.uio.no/ifi/texcount/) provides much more details

{% highlight bash %}
texcount -inc -total template.tex
Total
Words in text: 5409
Words in headers: 78
Words outside text (captions, etc.): 398
Number of headers: 25
Number of floats/tables/figures: 9
Number of math inlines: 44
Number of math displayed: 1
Files: 12
{% endhighlight %}

the option -inc includes all tex files recursivly and -total combis the statistics. To see the statics for each tex file leave out the -total option. 
