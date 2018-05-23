---
layout: post
category: github
tags: github jekyll blogging posting nextcloud
title: Getting Github Pages to Work right
---

There's a lot to do here to make this work. Here we go.

# Github Pages Plug in
First, the gh-pages plug in is apparently useful. Getting it to install is a
pain. Basically a high version of it needs to be specified, and then version
suggestions removed from other gems, then `bundle update`.

# Things just started working
So some things started working (the index page, the posts), but ~~other things
now aren't working (categories, tags).~~ It is working: I forgot to put
`.html` at the end of the url. ~~But the /category/THING page does work.~~
Of course now it says posts twice so you win some you lose some. This seems to
be some kind of auto title detection using the first heading. Simple solution
is to change the title of the page and delete the title.

# ~~Broken thing~~ Fixed thing
It seems that a different version of liquid or jekyll ~~doesn't support the
reversed keyword, so the posts are in chronological order, not reverse.~~
It would seem that reverse chronological is now the default behavior, so
reversed is not necessary. Cool.

# .gitignore
Note to self: Nextcloud seems to ignore dotfiles (at least sometimes) and
didn't get the .gitignore and it wasn't copied. Make sure \_site is in
.gitignore.


# Basically Working
As usual I was making things harder than they needed to be
