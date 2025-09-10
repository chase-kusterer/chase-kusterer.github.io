---
title: "From Print to Prediction"
excerpt: "A Beginner's Guide to Data Analysis in Python"
header:
  teaser: /assets/images/teasers/textbook_card.png
tags: [python, ml, analytics, textbook]
---

{% capture readme_raw %}{% include readmes/textbook/README.md %}{% endcapture %}

{% comment %} Split into lines and rebuild without the first line (the H1) {% endcomment %}
{% assign lines = readme_raw | split: "\n" %}
{% assign readme_wo_h1 = "" %}
{% for line in lines %}
  {% unless forloop.first %}
    {% assign readme_wo_h1 = readme_wo_h1 | append: line | append: "\n" %}
  {% endunless %}
{% endfor %}

<div class="readme">
  {{ readme_wo_h1 | markdownify }}
</div>
