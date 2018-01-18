---
layout: post
title: "Git aware prompt"
description: "Easily setup git-aware prompt in terminal."
categories: [tutorial]
tags: [git,prompt,autocomplete,terminal]
---

## Setting up git-aware prompt

Working with Git is impressive, although regularly switching branches, check out, commit is bothersome. Every time you have to copy paste long branch's name or run `git status` to see where your working one is dirty, or `git branch` see a list of branches.

The answer to this is to have the terminal furnished with a autocomplete function. It can:

- Autocomplete branch/command and everything else.
- See your current working branch
- Let you know if your current working branch is dirty or not

A Gif worths a thousand gifts, see the following and feel.

![git-aware.gif](/assets/images/gifs/git-aware.gif){:width="70%"}

## How to install

Go to your bash terminal and run:

~~~ bash
curl -sL https://raw.githubusercontent.com/bri0/git-aware-prompt/master/install.sh | sh -
~~~

After that, please restart your terminal.

If you `cd` to a Git working directory, you can see the current Git branch name displayed in your terminal prompt. When you are not in a Git working directory, your prompt works like usual.

You can also use tab to autocomplete your branch names

Please let me know if the install does not work for you.