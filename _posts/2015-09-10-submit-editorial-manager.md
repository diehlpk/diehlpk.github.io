---
layout: post
title: Submitting to Editorial Manager
tags:
  - Research
---
After successfully compiled a manuscript to the Editorial Manager including PDF images,
I like to provide some helpful comments to get your submission compiled.
<p>
<ol>
<li>Provide all files (.bst,.clo and .cls) tagged as manuscript item.</li>
<li>Upload only <bf>one</bf> .tex file, including all your LaTeX sources.</li>
<li>Use a flat folder structure and no subfolders.</li>
<li>Do not use "./image.pdf" in the path to the images.</li>
<li>Uncomment "/usepackage{todonotes}".</li>
<li>Tagg all "*.pdf" as figure item.</li>
<li>Insert at the top of the .tex file this line "%&pdflatex"</li>
</ol>
You should check <a href="http://www.editorialmanager.de/pdf/latex/LaTeX-Styles-on-EM-PDF-Builder-2013.pdf">here</a> if all your used packages are installed on there system.

Note, that they according to the <a href="http://www.edmgr.com/robohelp/current/EM_Knowledge_Base/Preparing_of_a_Tex_Submission_for_Editorial_Manager.htm">tutorial</a> are using Tex Live 2011, but in the error log it is Tex Live 2015.   
{% highlight bash %}
This is pdfTeX, Version 3.14159265-2.6-1.40.16 (TeX Live 2015/W32TeX)
(preloaded format=pdflatex 2015.7.29) 10 SEP 2015 13:13
{% endhighlight %}

If your build fails you are getting a e-mail "Unable to build PDF", that they were unable to build your PDF, but without any error log. To get the error log of the compilation process, I deleted all files and just uploaded the .tex file to the system and then got a message that "Your PDF has been build". At the website there was  an PDF file containing the error log of the compilation process. With these additional information I was able to compile and generate the PDF at the local machine. After adding all missing images I got a PDF without the references. After uploading the .bib file and compiling it again, the PDF file was complete for submission and I could approve it. 
