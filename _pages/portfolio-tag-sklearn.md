---
title: "Portfolio · scikit-learn"
permalink: /portfolio/sklearn/
layout: single
classes: wide
---
{% assign filtered = site.projects | where_exp:"p","p.tags contains 'sklearn' or p.tags contains 'scikit-learn' or p.tags contains 'scikitlearn'" %}
<div class="entries-grid">
  {% for project in filtered %}
    {% include archive-single.html type="grid" post=project %}
  {% endfor %}
</div>
