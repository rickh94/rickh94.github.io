---
title: Start Automating Creation of Posts
layout: post
category: python
tags: python jekyll github scripting
---
I have started creating the script to make and search blog posts (the creation of the posts is likely to be much easier).
It can create the tag files and category files and skeleton the post file, as well as checking all of this into git. Mostly
it's all in one file for now, but once the searching begins, all hell might break loose.

Important notes:
gitpython does NOT like Path objects, they must be converted to strings
The index object is very important in gitpython, most of the usual commands are done to it.
