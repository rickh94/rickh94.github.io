---
layout: post
title: Creating index and category pages with post excerpts
categories: jekyll
tags: blogging jekyll pages liquid
---

Creating an index.md with posts and excerpts was fairly straightforward,
though I cannot figure out what jekyll is doing to the # headings in markdown.
Oh well, trial and error.

The code snippet for the posts is fairly simple:
{% highlight liquid %}
{% raw %}

# Posts
{% for post in site.posts reversed %}
#### [{{ post.title }}]({{ post.url | absolute_url }})
{{ post.excerpt }}


{% endfor %}

{% endraw %}{% endhighlight %}

Note that to get reverse chronological (the only sensible way to list blog
posts), the `reversed` keyword is necessary (thank you stackoverflow).

# Category
The code for the category layout is almost the same as the code for index.md,
but in html. Layouts MUST be in html:

{% highlight liquid %}
{% raw %}

# Posts

---
layout: page
---

<h1>Posts</h1>
{% for post in site.categories[page.category] reversed %}
<a href= "{{ post.url | absolute_url}}">{{ post.title }}</a>
{{ post.excerpt }}

{% endfor %}

{% endraw %}{% endhighlight %}

It also requires a file to be created in the category folder with the layout
category as a blank file with only frontmatter, called the name of the
category and belonging to that category (frankly it seems like a bit of a hack).
This is how the creation of pages works in general, more or less. It also
works for tags in the same way.
The creation of these pages should be easy to automate.

I have also created centralized tags.html and categories.html that link to the
existing categories/tags.

