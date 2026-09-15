---
title: "Portfolio · Data Science"
permalink: /portfolio/data-science/
layout: single
classes: wide
---

<div class="entries-grid">
  {% for project in site.projects %}
    {% if project.tags contains 'data-science' or project.tags contains 'data science'%}
      {% include archive-single.html type="grid" post=project %}
    {% endif %}
  {% endfor %}
</div>
