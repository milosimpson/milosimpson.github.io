---
# You don't need to edit this file, it's empty on purpose.
# Edit theme's home layout instead if you wanna make some changes
# See: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
#layout: home

layout: default
title: Milo Simpson | Milo Simpson
---

# Milo Simpson

- [GitHub](https://github.com/milosimpson)

## Blog

[All posts](/blog.html)
{% for post in site.categories.tech limit: 3 %}
- `{{ post.date | date: "%Y-%m-%d" }}` - [{{ post.title }}]({{ post.url }}) {% endfor %}

## Projects

- [Jolt](https://github.com/bazaarvoice/jolt), a Java Json to Json transform tool
