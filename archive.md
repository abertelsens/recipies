---
permalink: /archive
layout: page
title: Archive
---
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{ post.content | strip_html | truncatewords: 50 }}
    </li>
  {% endfor %}
</ul>