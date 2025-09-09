---
title: "Portfolio · ML"
permalink: /portfolio/ml/
layout: single
classes: wide
---
{% assign filtered = site.projects | where_exp:"p","p.tags contains 'ml' or p.tags contains 'machine-learning' or p.tags contains 'machine learning'" %}
<div class="entries-grid">
  {% for project in filtered %}
    {% include archive-single.html type="grid" post=project %}
  {% endfor %}
</div>
