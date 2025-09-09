---
title: "Portfolio · html5"
permalink: /portfolio/sklearn/
layout: single
classes: wide
---
{% assign filtered = site.projects | where_exp:"p","p.tags contains 'html5' or p.tags contains 'html-5' or p.tags contains 'h5'" %}
<div class="entries-grid">
  {% for project in filtered %}
    {% include archive-single.html type="grid" post=project %}
  {% endfor %}
</div>
