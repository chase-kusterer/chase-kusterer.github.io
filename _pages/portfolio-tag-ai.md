---
title: "Portfolio · AI"
permalink: /portfolio/ai/
layout: single
classes: wide
---

<div class="entries-grid">
  {% for project in site.projects %}
    {% if project.tags contains 'ai' or project.tags contains 'artificial-intelligence' or project.tags contains 'artificial intelligence' %}
      {% include archive-single.html type="grid" post=project %}
    {% endif %}
  {% endfor %}
</div>
