
# Today I learned

<ul>
{% for page in site.til %}
      <li>
        <a href="{{ page.url }}">{{ page.title }}</a>
        <p>{{ page.hook }}</p>
      </li>
{% endfor %}
</ul>
