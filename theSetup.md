---
layout: default
---

# The Setup

Documenting how I setup all the things.

{% for page in site.theSetup %}
- `{{ page.date | date: "%Y-%m-%d" }}` - [{{ page.title }}]({{ page.url }}) {% endfor %}

