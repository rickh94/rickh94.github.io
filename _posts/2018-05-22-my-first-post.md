---
layout: post
title: Creating a Post in Jekyll
categories: jekyll
tags: blogging jekyll markdown posting liquid
---

This is my first blog post created for jekyll. Hopefully this
can be automated and generated more easily in the future so I can just type.
This is simply a markdown file in the `_posts` directory.

I used the command:
{% highlight bash %}
$ vim (date +%Y-%m-%d)-my-first-post.md
{% endhighlight %}
to create it.


## Some useful things:

# Frontmatter

Yaml frontmatter, set off by triple hyphens, is required on blogs. layout,
title, categories, and tags should each be set.

Note that categories are hierarchical, so `categories: jekyll blogging` is
made available under /jekyll/blogging/, maybe better to use tags for most
things.

# Adding an image:

![Screenshot1]({{ "/assets/screenshot1.png" | absolute_url }})

{% highlight markdown %}
{% raw %}
![Screenshot1]({{ "/assets/screenshot1.png" | absolute_url }})
{% endraw %}
{% endhighlight %}

A similar method can be used to include downloadable files.

# Code Highlighting
{% highlight liquid %}
{% raw %}
{% highlight WHATEVER %}{% endhighlight %}
{% endraw%}
{% endhighlight %}

# Variable insertion

Variables can be defined in the frontmatter, or elsewhere, and can
be called using curly braces and percent sign. Curly brace and percent sign
notation can also be used for code snippets like loops.

# Liquid

If literal liquid (curly braces and parentheses) is needed,
{% raw %}{% raw %}{% endraw %} can be used with and endraw later.

When using a {% highlight liquid %}{% raw %}{% highlight %}{% endraw %}{% endhighlight %} block, backticks are not
required for code formatting, but a newline is always added.


# Reminders about Markdown

  1. more #s = smaller. I was right, though jekyll or the theme definitely does something weird with the headers.
  8. Numbers in numbered lists don't matter, just that they are numbers.
  2. `[displaything](linktothing)`
  3. [Markdown
     Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
