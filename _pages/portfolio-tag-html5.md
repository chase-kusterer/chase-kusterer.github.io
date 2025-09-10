---
title: "Portfolio · HTML5"
permalink: /portfolio/html5/
layout: single
classes: wide
---

<div class="entries-grid">
  {% for project in site.projects %}
    {% if project.tags contains 'html5' or project.tags contains 'html' %}
      {% include archive-single.html type="grid" post=project %}
    {% endif %}
  {% endfor %}
</div>
