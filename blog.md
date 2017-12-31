---
layout: default
title: Milo Simpson | Blog
---

# Blog

{% for post in site.posts %}
- `{{ post.date | date: "%Y-%m-%d" }}` - [{{ post.title }}]({{ post.url }}) {% endfor %}
