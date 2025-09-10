---
title: "From Print to Prediction"
excerpt: "A Beginner's Guide to Data Analysis in Python"
header:
  teaser: /assets/images/teasers/textbook_card.png
tags: [python, ml, analytics, textbook]
---

{% capture readme_raw %}{% include readmes/textbook/README.md %}{% endcapture %}
{% assign lines = readme_raw | split: "\n" %}
{% assign readme_wo_h1 = "" %}
{% for line in lines %}
  {% if forloop.first and line contains "# " %}
    {# skip README's top H1 #}
  {% else %}
    {% assign readme_wo_h1 = readme_wo_h1 | append: line | append: "\n" %}
  {% endif %}
{% endfor %}
<div class="readme">
  {{ readme_wo_h1 | markdownify }}
</div>
