---
layout: default
---

# The Setup

Documenting how I setup all the things.

<ul>
{% for page in site.theSetup %}
      <li>
        [{{ page.title }}]({{ page.url }})
        <a href="{{ page.url }}">{{ page.title }}</a>
        <p>{{ page.hook }}</p>
      </li>
{% endfor %}
</ul>
