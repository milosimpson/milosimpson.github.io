---
layout: default
---

# The Setup

Place to document how various things are setup that is "latest" configuration.

<ul>
{% for page in site.theSetup %}
      <li>
        <a href="{{ page.url }}">{{ page.title }}</a>
        <p>{{ page.hook }}</p>
      </li>
{% endfor %}
</ul>
