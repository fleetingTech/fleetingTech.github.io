---
permalink: /archive
layout: page
title: Archive
---

<p>All posts sorted by Date.</p>
<ul>
  {% for post in site.posts %}
    <li>
      <a href=".{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
