---
title: Reboot unavailable Pi
layout: post
category: raspberrypi
tags: raspberrypi python monitoring reboot ssh
---

I want to run a nextcloud server on a raspberry pi at home but it the pi
sometimes loses its network connection for no apparent reason, and needs to be
manually rebooted. Based on other tools and some blog posts, I wrote some
[simple python scripts](https://github.com/rickh94/offline_auto_reboot) to automatically do this (with some ssh).

# Functionality

Basically there is the pi to reboot (it runs the reboot.py) and the external
pi. The external pi uses ssh to touch /tmp/online on the server to reboot and
the server checks the accessed time of that file. If it is longer ago than the
configured time, it reboots itself. My current timing runs the external every
half hour and the server checking every hour, configured to reboot if the file
is an hour old. I still need to configure them to do each other the other way,
I could get into a weird reboot loop if the one that's supposed to be touching
the file goes offline. It also leaves a file in /var/tmp if it reboots, so
that the reboot destroying the tempfile doesn't cause it to just keep
rebooting over and over because the file is missing. The flow control was a
little wonky, but I think I got it working.

# Security

Although reboot.py (the server monitoring file that reboots the server) has to
be run as root, it's better to have a dedicated user to run the ssh and touch
commands for security reasons.

# Weirdness

On one server (brahms), ruamel.yaml did not want to import from the system
path, so it's setup to run from a virtualenv, all in /root. Yay virtualenvs.

I played with some python libraries to do the ssh-ing but it seems that when
you don't want to do complicated stuff, subprocess.run() is the best option,
plus it keeps the dependencies low.
