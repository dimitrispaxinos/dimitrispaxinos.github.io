---
layout: page
title: Archive
---

<table class="archivetable">
{% for post in site.posts %}
<tr>
<td><a href="{{ post.url }}">{{ post.title }}</a>
<td style="text-align:right;">{{ post.date | date: '%B %d, %Y' }}	</td>
</tr>
{% endfor %}
</table>

