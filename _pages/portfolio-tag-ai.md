---
title: "Portfolio · AI"
permalink: /portfolio/ai/
layout: single
classes: wide
---
{% assign filtered = site.projects | where_exp:"p","p.tags contains 'ai' or p.tags contains 'artificial-intelligence' or p.tags contains 'artificial intelligence'" %}
<div class="entries-grid">
  {% for project in filtered %}
    {% include archive-single.html type="grid" post=project %}
  {% endfor %}
</div>
