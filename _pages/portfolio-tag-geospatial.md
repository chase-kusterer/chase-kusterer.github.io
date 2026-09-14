---
title: "Portfolio · Geospatial"
permalink: /portfolio/geospatial/
layout: single
classes: wide
---

<div class="entries-grid">
  {% for project in site.projects %}
    {% if project.tags contains 'geospatial' %}
      {% include archive-single.html type="grid" post=project %}
    {% endif %}
  {% endfor %}
</div>
