---
layout: page
title: Tags
---
<p>

<ul class="tags">
  {% for tag in site.tags %}   
  <li><a class="tag" href="/tags/{{ tag[0] }}">{{ tag[0] }}</a></li>
  {% if forloop.last != true %} {% endif %} {% endfor %}
</ul>  