---
title: "Portfolio · ML"
permalink: /portfolio/ml/
layout: single
classes: wide
---

<div class="entries-grid">
  {% for project in site.projects %}
    {% if project.tags contains 'ml' or project.tags contains 'machine-learning' or project.tags contains 'machine learning' %}
      {% include archive-single.html type="grid" post=project %}
    {% endif %}
  {% endfor %}
</div>
