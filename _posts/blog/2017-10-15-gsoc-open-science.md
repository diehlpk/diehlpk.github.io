---
layout: post
title: Open science session @ GSoC 2017
categories: blog
tags: [science]
author: diehlpk
---
This Google Summer of Code mentor summit there was a productive discussion of opportunities and challenges for open science. Here, I summarized the results of this discussion and like to mention these ideas are the contribution of the audience.

## Open source software
One topic of the discussion's agenda was the why do people, in our case especially researcher, decide to go for proprietary software. These are the points we could determine, including the audience experience made at their institutions.

* Mostly if people search for an open source alternative, they find either one side of the coin. On the front side of the coin is the situation that they find not any suitable open source solution. On the back side is the situation that there ate too many options. Most of them not mainly maintained, e.g. only by one developer. Which comes to the next point,  that for closed software the vendor comes with a guarantee for support. Where as for open source projects with a small community there is no such a guarantee and even worse no guarantee that the software will be maintained for the next years. 
* Also in many cases the education systems, e.g. the UK system has strict regulations to the software catalog, leads future researchers or employees into proprietary software. In most courses closed source software, i.e. Matlab and Maple, is introduced to students for solving their exercises. In this case good open source alternatives, like Octave and Maxima, which are compatible with the proprietary equivalences are available. This influences students for their career and the get addicted/hooked to this software. For example for these to open source alternatives, the learning curve is flat because the syntax is very similar to the closed source one. Another reason is that scientists are often very busy and do not have the time or energy to learn a new software. These issues are strongly related to the power of lobbying which open source communities can not do due to lack of costs. 
* Another aspect is liability which is important for pharmaceuticals or medicine. Here, the software company can be sued because they provide warranty that their implementation of algorithm are correct. Most open source projects have a warranty disclaimer in their licenses.
* A common problem is most institutions Windows and Mac OS X is most common and when it comes to Linux there is a lacking institutional support. One key point is that some open source software works very well on Linux because most developers are using Linux.

### Opportunities

* Having access to the source code can beneficial for finding bugs or gain insight how the algorithm is implemented. Imagine you get strange results with a closed source code and you do not have access to the source code. So it is quite hard to decide if there is a bug in the code or some curiosity in your data. In this case you could have a look into the source code and validate if there is an bug or how the algorithm works exactly. 
* Working with industrial partners or collaborators can lead that they direct you to use proprietary software. In this case some of proprietary software is compatible with open source solutions, e.g. LibreOffice with Microsoft Word and Octave with MatLab.
* To make it easier for specific disciplines, there are discipline-specific Linux distributions, i.e [Scientific Linux](https://www.scientificlinux.org/) for Scientific computing, [Bio Linux](http://environmentalomics.org/bio-linux/) for bioinformatics, and [Fedora Scientific](https://fedoraproject.org/wiki/Scientific_Spin) for general purpose in science. These distributions have the most common open source software pre-installed. 
* Provide a virtual machine with Linux and configure it such that all programming exercises can be done with this machine. Students can download this machine and use Linux inside of their common operating system. First, it makes it easier for them to get in touch with Linux and open source software. Second, it also promotes reproducibility for science.
* Windows 10 Linux subsystem can be used to install a Linux distribution within Windows. So people can install native Linux packages and run software directly on Linux. It is a nice workaround if your department does not support Linux. 
* Google Summer of Code PhD community stabilization -- great opportunity to provide PhD students to focus on proving their research software to the open source community. Mostly, this kind of work is not appreciated by the supervisors. 


## Open data and open access

The second topic on our agenda was open data and open access. The credibility for a scientist is the amount of publication, mostly in renowned peer-reviewed journals. Especially for junior fellows it is important to get these publications to get a permanent position in academia. The tax payer who found the research while paying taxes to the government has to pay several times. First, the researchers to do the science, second the reviewers to do the review, and last for the subscription of the library to the publishers. Another aspect is the data which is used in the publications or the source code to produce the results. Mostly these artifacts are not published with the publication, even if the could be used for reproducibility and validation of the published results. 

Here, you find the key problems out of this discussion

* Most tools for references/citation, e.g. Google Scholar and Web of Science, are proprietary and can’t be accessed by open source citation tools like Zenodo to add value to these kinds of citations.
* It would be great to have citation dependency graphs,like Web of Science provides for publications, for software and data would improve open source discoverability, Here, it would be great if the could integrate the data from initiatives, like Zenodo.
* Provide facilitating citations, like Altmetrics -- automated tools for determining how software or data is cited. Zenodo is involved in work on an open alternative for software citations.



### Opportunities

* Nowadays, it is more and more common that requirements of openness and reproducibility are defined by journals, institutions, and funding agencies. For example the [German government](https://www.bmbf.de/de/hilfe-bei-kosten-fuer-open-access-4722.html?pk_campaign=RSS&pk_kwd=Pressemeldung) provide a grant where researchers could apply for funding to pay for open access options for publications of previous projects. In some countries all governmental funded research has to be published as open access.
* [Zenodo](https://zenodo.org) is converting data and software into academic currency by providing Digital Object Identifier (DOI). Now, the item is citable like a publication and maybe in future citations for data and software are taken into account for the reputation of a researcher. 
* [The Journal of Open Source Software](http://joss.theoj.org/) peer-reviewed publishing of research software and obtaining a DOI after acceptance.
* Publishing open access -- continue to lobby aggressively for it; ask institutions (especially libraries -- they want open access so they can save on journal subscription costs), funding agencies for funding.
* Some programming languages, e.g. duecredit for pyhton, or documentation tools, like doxygen, provide possibilities to cite publications or software within the source code. 
* More meetings like this one here ;)

## Collection of links

* [Bullied Into Bad Science](http://bulliedintobadscience.org/) -- Initiative to promote and support open publication practices by PhD students and Postdoc
* [Colper science](https://colperscience.com/) -- Podcast which aims at promoting open science and efficient scholarly communications through its social media and podcasting. 
* [Code for Science and Society](https://codeforscience.org/) -- Supporting public data and technology through software development, education and outreach. 
* [Mozilla Open Leaders](https://mozilla.github.io/leadership-training/) -- Mentorship and Training on Working Open
* [Mozilla Science Lab](https://science.mozilla.org/) -- Mozilla Science Lab is a community of researchers, developers, and librarians making research open and accessible.


