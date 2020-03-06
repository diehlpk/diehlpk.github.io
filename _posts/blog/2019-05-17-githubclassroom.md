---
layout: post
title: Using Github classroom for assignments
categories: blog
tags: [Teaching]
author: diehlpk
---


### Requirements 

* Get a [github](https://github.com/) account. I recommend to use a username reflecting your name. 
* Install [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) on your development machine. 

### Setup github

```bash
git config --global user.name Surname Name
git config --global user.email you@provider.com
```

### Generate a ssh key

This step is only necessary, if you do not want to enter your password each time you work on github.

```bash
ssh-keygen -t rsa -C "you@provider.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/diehlpk/.ssh/id_rsa): ~/.ssh/id_rsa_github
ssh-add ~/.ssh/id_rsa_github
```

Copy the content of the ~/.ssh/id_rsa_github and add it to your github profile going to your profile -> SSH keys and GPG keys -> New SSH key.

### Working on your assignment

For each assignment you will get an e-mail and find the link to your assignment on the exercise sheet. 

![GitHub Logo]({{ site.url }}/assets/2019-05-17-github-assingment.png)

After clicking on the link you will get the url to your git repository.

![GitHub Logo]({{ site.url }}/assets/2019-05-17-github-invitation.png)

Use the commands to checkout and submit your homework.

```bash
git clone https://github.com/diehlpkteaching/test-diehlpk.git
cd test-diehlpk
touch exercise.cpp
git add exercise.cpp
# Work on your exercise
git commit -a
git push
```

Note that you can commit and push your work as often as you want. I recommend commit and push often to save your work and have a history.

### Video tutorial 

[![asciicast](https://asciinema.org/a/308129.svg)](https://asciinema.org/a/308129)


