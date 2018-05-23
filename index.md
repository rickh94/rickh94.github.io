---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: page
---

# Posts
{% for post in site.posts reversed %}
#### [{{ post.title }}]({{ post.url | absolute_url }})
{{ post.excerpt }}


{% endfor %}
