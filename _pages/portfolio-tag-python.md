---
title: "Portfolio · Python"
permalink: /portfolio/python/
layout: single
classes: wide
---

<div class="entries-grid">
  {% for project in site.projects %}
    {% if project.tags contains 'python' %}
      {% include archive-single.html type="grid" post=project %}
    {% endif %}
  {% endfor %}
</div>
