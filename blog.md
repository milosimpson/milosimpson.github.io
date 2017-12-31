---
layout: default
title: Milo Simpson | Blog
---

# Blog

{% for post in site.categories.tech %}
- `{{ post.date | date: "%Y-%m-%d" }}` - [{{ post.title }}]({{ post.url }}) {% endfor %}
