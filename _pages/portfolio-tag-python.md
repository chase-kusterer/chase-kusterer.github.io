---
title: "Portfolio · Python"
permalink: /portfolio/python/
layout: single
classes: wide
---
{% assign filtered = site.projects | where_exp:"p","p.tags contains 'python'" %}
<div class="entries-grid">
  {% for project in filtered %}
    {% include archive-single.html type="grid" post=project %}
  {% endfor %}
</div>
