---
layout: post
title: "Tonny learns the MNIST"
description: "Practicing Deep Learning with MNIST set from the beginning (the hard way)"
categories: [deep-learning]
tags: [mnist,keras,python,theano,ccn]
---

Be warned: This article is not about Deep Learning, nor to teach you how to start with Deep Learning. Instead, this is a  step by step note of an experiment with one of the most famous tutorials of CNN network: MNIST. So if you find nothing else, just ignore this post.

Do not worry if you don't know the keyword or terminologies; I don't do either. All you need to do is just be stubborn, stick with it, see the result and figure out what they mean.
Nevertheless, expect some jump here and there since I assume you've already known some stuff.

## Prerequires

I'm running on MacOS Sierra, so you should expect there are some differences if Windows is your choice. Also, you must know to open up Terminal.

## Step 1: Install Python

Start by typing Python in your Terminal, if it is a not found command, consider installing it. Of course, Python with a version manager is the best choice. For me:

~~~ bash
$ python
Python 2.7.10 (default, Feb  7 2017, 00:08:15)
[GCC 4.2.1 Compatible Apple LLVM 8.0.0 (clang-800.0.34)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
~~~

Oh no, is this the system Python? I need the Anaconda Distribution of Python for a reason you will know in other future articles. So first I need to install Python Version Manager; I guess you already know some similar kinds of stuff for different languages. Literally, like `nvm` for `node.js` or `rvm` for `ruby` language. A quick search on Google leads me to the https://github.com/pyenv/pyenv repository.

## Step 2: Install `pyenv` with Homebrew

~~~ bash
$ brew update
$ brew install pyenv
~~~

After several minutes, quick check if `pyenv` got installed or not:

~~~
$ pyenv -h
Usage: pyenv <command> [<args>]

Some useful pyenv commands are:
   commands    List all available pyenv commands
   local       Set or show the local application-specific Python version
   global      Set or show the global Python version
   shell       Set or show the shell-specific Python version
   install     Install a Python version using python-build
   uninstall   Uninstall a specific Python version
   rehash      Rehash pyenv shims (run this after installing executables)
   version     Show the current Python version and its origin
   versions    List all Python versions available to pyenv
   which       Display the full path to an executable
   whence      List all Python versions that contain the given executable

See `pyenv help <command>' for information on a specific command.
For full documentation, see: https://github.com/pyenv/pyenv#readme
~~~

So far so good.

## Step 3: Install python with `pyenv`

Let's search for a pyenv version with python

~~~ bash
$ pyenv install -l | grep anaconda
...
 anaconda-4.0.0
...
~~~

Ok, let's choose version 4.0.0

~~~ bash
$ pyenv install anaconda-4.0.0
$ pyenv global anaconda-4.0.0
~~~

Let's do the final check

~~~ bash
 $ python --version
Python 2.7.10
$ which python
/usr/bin/python
~~~

Not this time, os still uses system version, let's check if pyenv uses anaconda or not.

~~~ bash
$ pyenv versions
  system
* anaconda-4.0.0 (set by /Users/tonny/.pyenv/version)
~~~

So far so good, what's missing? Maybe the path to the anaconda Python? Let check:

~~~ bash
$ pyenv which python
/Users/tonny/.pyenv/versions/anaconda-4.0.0/bin/python
$ echo $PATH | grep `pyenv which python`
~~~

Ok, that's the problem, let's fix it.

~~~ bash
~ $ echo 'eval "$(pyenv init -)"' >> ~/.profile
~ $ . ~/.profile
~ $ python --version
Python 2.7.11 :: Anaconda 4.0.0 (x86_64)
~~~

Ok so far so good this time

So sleepy .zZ See you next time
