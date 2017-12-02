---
layout: post
title: Open science session @ GSoC 2017
categories: blog
tags: [science]
author: diehlpk
---

_This post was co-authored by Alexey Shiklomanov ([web](https://ashiklom.github.io)), who was the lead organizer of the session. The session was co-organized by Betsy Cowdery (Boston University; PEcAn Project) and Krzysztof Nowak (Zenodo)._

At this year's Google Summer of Code mentor summit, there was a productive discussion of opportunities and challenges for open science. Here is a summary of the results of this discussion, including many valuable ideas and resources contributed by the large and diverse audience.

## Open source software

The first major topic of discussion was: Why do researchers (and people in general) use proprietary software?
This led to an insightful discussion of both the challenges faced by open source software, as well as opportunities afforded by it.

### Challenges

* In some specific cases, there are no viable open source solutions. The example from one audience member was special proprietary software used for advanced physics simulations (unfortunately, we didn't write down the name).
* Meanwhile, in other cases, there are _too many_ open source solutions, each maintained by a small group of volunteers, a single developer, or nobody at all. For one, this fragmentation forces users to decide between multiple options with effectively zero guidance. Moreover, even the best-maintained among such projects cannot provide the same level of maintenance and technical support as their commercial, proprietary counterparts.
* Sometimes, software decisions are regulated by institutions. For instance, the United Kingdom's educational system has a limited catalog of software available for use in the classroom. Commercial software companies (e.g. Matlab for engineering, Maple for mathematics) have the resources to lobby for their software to make it through these restrictions, whereas open source alternatives (e.g. Octave and Maxima, respectively) lack these resources. A consequence of limiting education to commercial software means that students become accustomed to specific proprietary software packages early in their careers and are unlikely to switch to open source alternatives later in life when they do not have the time, energy, or incentive to learn the new software.
* Particularly in disciplines with strong commercial applications, such as engineering, finance, and medicine, software liability is an important issue. Commercial software packages often have legal guarantees that their implementations of algorithms are accurate. On the other hand, even major open source projects are distributed with warranty-free licenses such as MIT and GNU General Public License (GPL) that offer no such guarantees.
* Institutional support (e.g. IT, Tech Support) for open source software often lags considerably behind support for proprietary software. For instance, the Windows and Mac OS operating systems are much better supported by tech support desks of most educational institutions than Linux distributions, probably in large part because of the official support from parent companies Microsoft and Apple. Meanwhile, open source software is often developed exclusively for Linux and has no ports for Windows or Mac OS.

### Opportunities

* Users that get strange results from their open source software are free to inspect the source code to look for bugs and issues with algorithm implementation. Tech-savvy users may even fix these issues and submit the fixes upstream. On the other hand, users that get strange results from closed-source software will have much more difficulty identifying bugs, and no opportunity at all to fix them.
* Open source software is often designed to be compatible with proprietary file formats. For instance, the open source office suite LibreOffice is capable of opening most documents produced in Microsoft Office. Similarly, GNU Octave is designed to be a drop-in replacement for MatLab. In fact, some open source software has a broader range of interoperability than any proprietary alternative, since open source developers have no incentive to monopolize markets by forcing users to use specific formats (as is often the case for proprietary software).
* The ability of communities to access the source code of open source software has led some to customize software packages for specific applications. Discipline-specific Linux distributions, such as [Scientific Linux](https://www.scientificlinux.org/) for scientific computing, [Bio Linux](http://environmentalomics.org/bio-linux/) for bioinformatics, and [Fedora Scientific](https://fedoraproject.org/wiki/Scientific_Spin) for general-purpose science, are great examples. Moving beyond software packages, these systems ship with many different but interoperable programs already pre-installed, providing users with a fully functioning computing ecosystem out of the box.
* The openness of Linux as an operating system makes it easy to create virtual machines with all relevant software and data pre-installed. This is useful in education by eliminating most of the overhead of software installation and configuration on multiple systems (and, as a bonus, provides students with exposure to Linux). This is also very useful for reproducible science by providing the exact set of tools (including specific versions of all relevant packages) required to perform a particular analysis.
* Some proprietary software is becoming more accommodating of its open-source counterparts. For example, the Windows 10 Linux subsystem provides native access to the Unix shell and many features of the Ubuntu Linux operating system natively on Windows, thereby allowing Windows users to run many native Linux packages side-by-side with Windows applications without the need for virtual machines. This should ease the transition for people interested in switching to open source software by allowing them to run some open-source programs without having to learn an entire new operating system.

#### A special opportunity: Google Summer of Code PhD community stabilization

One opportunity is important enough to be called out separately. 
PhD students in fields with a significant quantitative component often engage in software development without necessarily realizing it.
After all, most advanced data processing and analysis tasks required for research are now done in code.
Development and distribution of these codes as open-source software packages could be transformative in terms of reducing redundancy of effort, promoting collaboration, and the creation of more robust tools that in turn lead to better and more reproducible science.
However, PhD students currently have little incentive or support from their supervisors, institutions, or funding agencies for developing good open-source software.

Google's Open Source initiative, and Google Summer of Code in particular, is an excellent vehicle for providing this support.
For one, some PhD research tasks, such as data curation and algorithm optimization, could themselves be Google Summer of Code projects. 
This could significantly benefit both students and mentors; students would get exposure to the world of graduate-level academic research and perhaps even contribute to peer-reviewed publications, while the mentors (PhD students) would get valuable mentoring experience and benefit from the programming expertise of their students.
More generally, Google could provide incentives (e.g. grants, educational resources, cyberinfrastructure) and organizational support (e.g. social networking, platforms for code-sharing, mentor ship and code review) to PhD students developing or contributing to open source software.

## Open data and open access

### Challenges

Success in an academic career, especially for early-career scientists on the job market or applying for tenure, is strongly tied to the quantity and quality of publications in peer-reviewed journals. On the other hand, data and software produced by scientists are seldom considered, even though these contributions may be more significant and lasting. The inability to value data and software as contributions is a strong disincentive for scientists to make data and science openly and freely available, which in turn is an impediment to reproducibility and scientific progress as a whole. While extensive cyberinfrastructure does exist for quantifying scientists' contributions in terms of publications (e.g. Google Scholar, Web of Science), the same infrastructure is lacking for contributions in terms of data and software. Open source organizations like [Zenodo](https://zenodo.org/) are working hard to provide this infrastructure, but are hampered by the absence of accessible APIs to proprietary tools for aggregating publications like Google Scholar and Web of Science.

Meanwhile, another key barrier to open science is that most top-tier journals restrict access to their publications, thus forcing institutions to pay subscription fees or scientist authors to pay hefty fees to make their publications open access. This severely limits the ability of the general public and organizations lacking the resources to pay for journal subscriptions to access science, which is particularly ironic given the huge fraction of science that is publicly (i.e. taxpayer) funded.

### Opportunities

Despite the grim picture painted above, we were able to identify some key opportunities for improvement, which are as follows:

* [Zenodo](https://zenodo.org) is working to provide Digital Object Identifiers (DOIs) to not just papers, but also software and data. By making these contributions citable in the same way as publications, and by tracking and aggregating these citations (similarly to the proprietary Altmetrics service), Zenodo's hopes that software and data will eventually be taken into account when assessing a researcher's professional reputation. In addition, Zenodo is also working towards building tools like citation dependency graphs (similar to those provided by Web of Science) that include all citable output (i.e. publications, software, and data), thereby promoting software and data discoverability.
* Requirements of openness and reproducibility from journals, institutions, and funding agencies are becoming increasingly common. For example, the [German government](https://www.bmbf.de/de/hilfe-bei-kosten-fuer-open-access-4722.html?pk_campaign=RSS&pk_kwd=Pressemeldung) offers a grant to pay for open access options for publications of previous projects. In some countries, including the United States and the United Kingdom, certain agencies are starting to require that any research they fund has to be published as open access. However, until the practice of open-access publishing becomes universal, we need to continue to lobby actively for it and demand funding from institutions and funding agencies to cover open-access publication fees. Institutional libraries could be a great source for these initiatives; open-access publications are very much in the interest of libraries since they allow libraries to save on subscription costs.
* Journals specifically designed to promote open science practices are becoming more common. One great example is the [The Journal of Open Source Software](http://joss.theoj.org/), which performs peer-review of research software and its documentation and provides the software with a DOI upon acceptance.
* Some programming languages provide tools for making it easier to cite their software packages (e.g. `duecredit` for python, `cite()` function in R). In parallel, documentation software like doxygen provides possibilities for citing publications or software directly within the source code, thereby promoting reproducibility and openness.
* More meetings like this one here ;)

## Additional resources

* [Bullied Into Bad Science](http://bulliedintobadscience.org/) -- Initiative to promote and support open publication practices by PhD students and Postdocs
* [Colper science](https://colperscience.com/) -- Podcast aimed at promoting open science and efficient scholarly communications
* [Code for Science and Society](https://codeforscience.org/) -- Supporting public data and technology through software development, education and outreach. 
* [Mozilla Open Leaders](https://mozilla.github.io/leadership-training/) -- Mentorship and Training on Working Open
* [Mozilla Science Lab](https://science.mozilla.org/) -- Mozilla Science Lab is a community of researchers, developers, and librarians making research open and accessible.


